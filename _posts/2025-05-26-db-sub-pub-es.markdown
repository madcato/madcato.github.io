---
layout:     post
title:      "Arquitectura de procesos DB+Sub/Pub"
subtitle:   "Como crear un sistema de intercomunicación de procesos resiliente"
date:       2025-05-26 06:00:00
author:     "Daniel Vela"
locale:     es
lang-ref:   db-sub-pub
---

> Esta arquitectura la vi en funcionamiento en un sistema logístico que ofrecía servicio tanto a terminales de operarios, como a hardware electrónico de control de maquinaria. Me sorprendió lo resistente que era a los muchos problemas y fallos que nos íbamos encontrando.

La idea básica es la siguiente. Todo el sistema de control esta ejecutándose en diferentes procesos de diferentes máquinas dentro de una misma red. En dicha red, un servidor almacenaba todos los datos en una única base de datos centralizada. Cuando un proceso encontraba una nueva tarea, que otro servicio debía completar, creaba una nueva entrada en una determinada tabla almacenando todos los datos de la tarea. Seguidamente, realizaba una notificación por red al servicio, para indicarle que tenía una nueva tarea por cerrar. 

Parece ilógico que no se usara esa misma comunicación por red, no solo para notificar la tarea, sino también para indicar los datos a procesar. En vez de eso, los datos eran almacenados en una tabla en estado "a la espera". Esto parecería un mal gasto de recursos, hasta que te tienes en consideración la necesidad de construir sistemas resistentes a los fallos. 

# ¿Por qué DB+Pub/Sub es una buena opción?

La arquitectura DB+Pub/Sub es ideal para múltiples escenarios las siguientes razones:
1. **Resiliencia**: Los datos persisten en la base de datos, por lo que un fallo en cualquier gestor de chats, servicios, o la UI no resulta en pérdida de información.
2. **Desacoplamiento**: Los componentes no necesitan comunicarse directamente; la base de datos actúa como fuente de verdad, y las colas gestionan las notificaciones.
3. **Modularidad**: Puedes añadir nuevos componentes (como un módulo de análisis o un nuevo tipo de UI) sin cambiar la arquitectura.
4. **Escalabilidad**: Las colas permiten manejar cargas altas, y la base de datos centralizada soporta múltiples consumidores.
5. **Flexibilidad**: Puedes cambiar tecnologías (por ejemplo, de CoreData a PostgreSQL, Sqlite) sin afectar la lógica de comunicación.

Esta arquitectura es común en sistemas distribuidos (por ejemplo, microservicios) y es muy adecuada para comunicaciones no críticas en tiempo real, como el UI de presentación de datos.

# Diseño de la arquitectura DB+Pub/Sub

En esta arquitectura, la base de datos almacena los mensajes y el estado de la comunicación, y el sistema de colas pub/sub notifica a los componentes cuando hay trabajo pendiente (por ejemplo, un nuevo mensaje o un comando).

* **Base de datos centralizada**:
    - Almacena el estado de las conversaciones, la lista de chats, los comandos, los mensajes y las configuraciones.
    - También guarda los comandos enviados por la UI (como "seleccionar chat") y las actualizaciones generadas por el gestor de chats (como nuevos mensajes).
    - Ejemplos de tecnologías: PostgreSQL (para entornos distribuidos), MongoDB (para datos no estructurados), o incluso CoreData (si la UI está en un dispositivo local y no necesitas un servidor centralizado).
* **Sistema de colas**:
    - Actúa como un mecanismo de notificación para "despertar" a los componentes cuando hay datos nuevos en la base de datos.
    - Ejemplos de tecnologías: RabbitMQ, Kafka, o Redis (usando sus capacidades de colas o Pub/Sub).
    - Cada componente (gestor de chats, UI) tiene su propia cola para recibir notificaciones.
* **Flujo de comunicación**:
    - De UI a gestor de datos:
        - La UI escribe un comando (por ejemplo, `{ "type": "select_chat", "chat_id": "123" }`) en la base de datos (en una tabla como `commands`).
        - La UI publica un mensaje en la cola del gestor de chats (por ejemplo, "nuevo comando para procesar").
        - El gestor de datos lee la notificación de la cola, consulta el comando en la base de datos, lo procesa (por ejemplo, actualiza el chat activo), y guarda el resultado en la base de datos.
    - De gestor de datos a UI:
        - El gestor de chats escribe una actualización (por ejemplo, un nuevo mensaje `{ "type": "new_message", "chat_id": "123", "text": "Hola" }`) en la base de datos (en una tabla como updates).
        - El gestor publica un mensaje en la cola de la UI (por ejemplo, "nueva actualización disponible").
        - La UI lee la notificación, consulta la base de datos, y actualiza la interfaz con los nuevos datos.

# Implementación práctica

Aquí tienes un esquema detallado para implementar un ejemplo de comunicación entre un gestor de chats y UI de usuario con DB+Sub/Pub:

1. Base de datos
    * Tecnología sugerida: PostgreSQL (escalable, robusto, compatible con entornos distribuidos) o CoreData (si la UI y el gestor están en el mismo dispositivo).
    * Esquema sugerido:
        - Tabla `chats`: Almacena la lista de chats (`chat_id`, `name`, `created_at`).
        - Tabla `messages`: Almacena los mensajes (`message_id`, `chat_id`, `text`, `timestamp`, `sender`).
        - Tabla `commands`: Almacena comandos de la UI (`command_id`, `type`, `data`, `status`, `timestamp`).
        - Tabla `updates:` Almacena actualizaciones del gestor de chats (`update_id`, `type`, `data`, `chat_id`, `timestamp`).
    * Ejemplo en PostgreSQL:

```sql
CREATE TABLE chats (
    chat_id VARCHAR(50) PRIMARY KEY,
    name VARCHAR(100),
    created_at TIMESTAMP
);

CREATE TABLE messages (
    message_id SERIAL PRIMARY KEY,
    chat_id VARCHAR(50) REFERENCES chats(chat_id),
    text TEXT,
    timestamp TIMESTAMP,
    sender VARCHAR(50)
);

CREATE TABLE commands (
    command_id SERIAL PRIMARY KEY,
    type VARCHAR(50),
    data JSONB,
    status VARCHAR(20), -- pending, processed
    timestamp TIMESTAMP
);

CREATE TABLE updates (
    update_id SERIAL PRIMARY KEY,
    type VARCHAR(50),
    data JSONB,
    chat_id VARCHAR(50),
    timestamp TIMESTAMP
);
```

1. Sistema de colas
    * Tecnología sugerida: RabbitMQ (fácil de usar, robusto) o Redis (más ligero, con Pub/Sub o colas).
    * Colas:
        - `ui_commands`: Para notificar al gestor de chats sobre comandos de la UI.
        - `ui_updates`: Para notificar a la UI sobre actualizaciones del gestor de chats.
    * Formato de mensajes en la cola:
        - Para comandos: `{ "command_id": 123, "type": "select_chat" }`
        - Para actualizaciones: `{ "update_id": 456, "type": "new_message", "chat_id": "123" }`
2. Gestor de chats (en Rust, Python, o similar)
    * Funcionalidad:
        - Escucha la cola `ui_commands`.
        - Cuando recibe una notificación, consulta la tabla `commands` en la base de datos, procesa el comando (por ejemplo, selecciona un chat), y actualiza el estado en la base de datos.
        - Cuando genera una actualización (por ejemplo, un nuevo mensaje), la escribe en la tabla `updates` y publica una notificación en la cola `ui_updates`.
    * Ejemplo en Python con RabbitMQ:

```python
import pika
import psycopg2
import json

# Conexión a la base de datos
db_conn = psycopg2.connect("dbname=chatbot user=postgres password=secret")
cursor = db_conn.cursor()

# Conexión a RabbitMQ
connection = pika.BlockingConnection(pika.ConnectionParameters("localhost"))
channel = connection.channel()
channel.queue_declare(queue="ui_commands")

def callback(ch, method, properties, body):
    command = json.loads(body)
    command_id = command["command_id"]
    cursor.execute("SELECT data FROM commands WHERE command_id = %s", (command_id,))
    data = cursor.fetchone()[0]
    
    if data["type"] == "select_chat":
        chat_id = data["chat_id"]
        # Actualizar chat activo (por ejemplo, en memoria o DB)
        cursor.execute(
            "INSERT INTO updates (type, data, chat_id, timestamp) VALUES (%s, %s, %s, NOW())",
            ("chat_selected", json.dumps({"chat_id": chat_id}), chat_id)
        )
        db_conn.commit()
        channel.basic_publish(exchange="", routing_key="ui_updates", body=json.dumps({"update_id": cursor.lastrowid}))

    cursor.execute("UPDATE commands SET status = 'processed' WHERE command_id = %s", (command_id,))
    db_conn.commit()

channel.basic_consume(queue="ui_commands", on_message_callback=callback, auto_ack=True)
channel.start_consuming()
```

4. UI (en Swift)
   * Funcionalidad:
        - Escucha la cola `ui_updates`.
        - Cuando recibe una notificación, consulta la tabla `updates` en la base de datos y actualiza la interfaz (por ejemplo, añade un nuevo mensaje).
        - Cuando el usuario realiza una acción (como seleccionar un chat), escribe el comando en la tabla `commands` y publica una notificación en la cola `ui_commands`.
    * Ejemplo en Swift con Redis (usando SwiftRedis):

```swift
import SwiftRedis
import Foundation
import SwiftUI

class ChatViewModel: ObservableObject {
    @Published var messages: [Message] = []
    let redis = Redis()
    let db = Database() // Conexión a PostgreSQL o CoreData

    init() {
        redis.connect(host: "localhost", port: 6379) { _ in
            redis.subscribe("ui_updates") { message in
                let update = try! JSONDecoder().decode(Update.self, from: message.data)
                self.fetchUpdate(updateId: update.updateId)
            }
        }
    }

    func fetchUpdate(updateId: Int) {
        let update = db.query("SELECT data, chat_id FROM updates WHERE update_id = $1", parameters: [updateId])
        if update["type"] == "new_message" {
            DispatchQueue.main.async {
                self.messages.append(Message(text: update["data"]["text"], chatId: update["chat_id"]))
            }
        }
    }

    func selectChat(chatId: String) {
        let command = ["type": "select_chat", "chat_id": chatId]
        let commandId = db.insert("INSERT INTO commands (type, data, status, timestamp) VALUES ($1, $2, 'pending', NOW()) RETURNING command_id", parameters: ["select_chat", command])
        redis.publish("ui_commands", message: ["command_id": commandId, "type": "select_chat"])
    }
}
```

1. Resiliencia
    * Persistencia: Los datos en la base de datos (tablas `commands` y `updates`) aseguran que no se pierdan comandos ni actualizaciones si un componente falla.
    * Recuperación: Si la UI o el gestor de chats se reinicia, pueden consultar la base de datos para recuperar el estado (por ejemplo, los últimos mensajes o comandos pendientes).
    * Reintentos: Configura las colas con reintentos automáticos (por ejemplo, en RabbitMQ) para manejar fallos temporales.
2. Optimizaciones
    * Índices en la base de datos: Crea índices en `commands.command_id`, `updates.update_id`, y `messages.chat_id` para acelerar consultas.
    * Colas separadas por usuario: Usa colas específicas por `session_id` o `user_id` para escalar en sistemas multiusuario.
    * Limpieza de datos: Implementa un mecanismo para eliminar comandos y actualizaciones procesados después de un tiempo (por ejemplo, con una tarea programada).
    * Caching local: La UI puede usar CoreData o un caché en memoria para reducir consultas a la base de datos.
