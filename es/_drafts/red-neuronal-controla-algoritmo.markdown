---
layout:     post
title:      "Cómo entrenar una red neuronal del que no conocemos sus resultados directos"
subtitle:   "spolier: neuroevolución generativa usando algoritmos genéticos"
date:       2022-11-02 00:00:00
author:     "Daniel Vela"
background: "/img/post-bg-02.jpg"
locale:     es
lang-ref:   neural-net-control-algorithm
---

Para poder entrenar una red neuronal artificial es imprescindible que todas operaciones matemáticas que realice deben ser derivables. El motivo es el modo de entrenamiento de estas redes. Los errores en la salida son propagados al resto de la red, para adaptar sus valores y reducir dicho error paulatinamente. Pero que pasaría si no dispusiéramos de las salidas de dicha red. ¿Cómo entrenaríamos la red?

# StackNNA
Supongamos el siguiente caso. Queremos entrenar una red que controle una [pila](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) que nos ayude a transformar ecuaciones especificadas en `in-orden` en formato `post-orden`.

Ejemplos:

>  "2 + 4" 							--> 	"2 4 +"    
>  "3 * 2 + 4" 						--> 	"3 2 * 4 +"    
>  "4 + 8 * 6 - 5 / 3 - 2 * 2 + 2" 	--> 	"4 8 6 * + 5  3 / - 2 2 * - 2 +"     
>  

_(Este problema podría resolverse con Transformers y otros algoritmos de IA iterativos. Pero para este caso usaremos una red básica con capas lineales.)_

## Solución
Para resolver este algoritmo necesitamos tres operaciones:
- **PUT**: mueve un carácter de la entrada a la salida.
- **PUSH**: mueve un carácter de la entrada a la pila.
- **POP**: mueve un carácter de la pila a la salida.

La red neuronal tendría dos entradas y tres salidas. Las entradas serían el siguiente carácter de la entrada y el carácter de la cabeza de la pila. Las salidas serían el comando que ejecutaría el algoritmo: **PUT**, **PUSH**, **POP**.

![StackNNA Diagram]({{ site.url }}/assets/stackNNA.png)
