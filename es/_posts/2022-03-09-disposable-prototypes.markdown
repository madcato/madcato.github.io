---
layout:     post
title:      "Prototipos desechables"
date:       2022-03-09 01:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-10.jpg"
locale:       es
lang-ref:   disposable-prototypes
---

Un prototipo desechable en un pequeño proyecto que se realiza para aprender algo. Un prototipo es tan grande como el problema que estudia. Cuando se inicia un código con el único objetivo de entender cómo funciona dicho código, podemos hablar de que hemos creado un prototipo desechable.

Hay diferentes motivos por los que invertir tiempo en crear uno de estos prototipos:
- Aprender a usar una librería o framework.
- Probar un diseño o arquitectura.

Un ejemplo de un prototipo desechable sería una pequeña app iOS para aprender a integrar el sistema de pagos Apple Pay. Es mejor crear una pequeña prueba de concepto, para así asimilar el funcionamiento de esta tecnología, con el objetivo de integrar dicha funcionalidad en una proyecto existente, el cual es más complejo de modificar que una app vacía. Otro ejemplo podría ser la integración de una autenticación OAuth.

Es muy importante entender, y aceptar, que un prototipo se compone de un código que no va a ser reutilizado. Ni otros proyecto deben usar estos códigos, ni tampoco este prototipo debe usarse para iniciar un nuevo proyecto. El motivo es que estos códigos deben hacerse deprisa y corriendo, con el único propósito de aprender algo. No hace falta escribir un buen código, pues esto haría que se tardara mucho en codificar. Tampoco es necesario definir correctamente los recursos gráficos, ni tampoco realizar un código seguro, ni cumplir las directrices definidas por los proveedores del sistema operativo o del entorno de programación. Solo se ha de programar el objetivo principal prototipo.

Por ello, el código de todo prototipo debe usarse exclusivamente como referencia. Merece la pena guardarlo, pero sólo con intenciones consultivas, solo para comprobar cómo se resolvió el problema.  

Lo realmente importante es dejar constancia de todos los descubrimientos y conclusiones en un documento de texto, como un fichero ‘readme.md’, donde se describe lo que se ha hecho, por qué, qué documentación y librerías se usaron, y por último, qué conclusiones se sacaron de este esfuerzo.
