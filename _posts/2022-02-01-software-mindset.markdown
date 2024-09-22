---
layout:     post
title:      "Mentalidad de software"
date:       2022-02-01 01:00:00
author:     "Daniel Vela"
background: "/img/post-bg-08.jpg"
locale:       es
lang-ref:   software-mindset
---

TExiste una aparente paradoja relacionada con el software que usamos como programadores. Técnicamente todo programador podría crear desde cero todo el software que necesita: pero hoy en día es prácticamente imposible crear todo ese software. Tendríamos que crear los sistemas operativos, lenguajes de programación, compiladores, librerías: esto no es posible, por ser demasiado tiempo de desarrollo.

Sin embargo, la opción opuesta a esta tampoco es aconsejable. Tratar de usar todo el software posible, creado por terceras personas, tampoco es una buena opción. Primero, usar software de terceros puede provocar introducir en tu sistema bugs o fallos de seguridad, o incluso explotación de datos no consentida: especialmente si el software es propietario, en vez de "open source". Además usar software de terceros te impide aprender a programar: hoy en día la programación se ha convertido en una mera "búsqueda por internet".

Hay muchas cosas que como desarrolladores podríamos hacer, pero como ingenieros no debemos. El motivo principal de esta criba es el tiempo. No podemos crear todo lo que necesitamos: hay software muy complejo, como sistemas operativos y bases de datos, que debemos usar lo que ya hay construido: construirlos desde cero sería un trabajo enorme.

Cribar hacia abajo es sencillo, hay mucho software de base que debe ser reutilizado. ¿Pero hacia arriba, cuál es la criba? ¿Cómo diferenciar aquellas librerías que no deben usarse?

Estos son algunos criterios que deben usarse:
- Nunca usar una librería, por muy cómoda y famosa que sea, cuando el sistema operativo o el framework de desarrollo ya dispongan de una alternativa funcional. Un ejemplo sería dejar de usar Alamofire, porque Foundation de iOS ya dispone de URLSessions, que es más que suficiente para todo el tema de red.
- Nunca usar librerías que no sean de código abierto. Es necesario controlar lo que se introduce en tu propio proyecto. Hay que controlar las versiones, estar al tanto de las actualizaciones de seguridad.
- Nunca usar librerías que no dispongan de una amplia comunidad de usuarios. Esto incluye disponer de buenos ejemplos de uso, guías y referencia: sin documentación no hay librería.
- Nunca usar una librería que solucione un punto clave de tu modelo de negocio. Las librerías de terceros suelen ser más difíciles de adaptar y mejorar que las propias. Cada negocio tienen necesidades clave que el software debe suplir. Estas necesidades provocan que el software deba ser adaptado o mejorado con asiduidad; por ello es imprescindible controlar dicho software al 100%. Un ejemplo de esto sería un sistema de venta: aquí es imprescindible disponer de un carrito de compra completamente programado por la empresa. Usar una librería de terceros de carrito de compra, podría introducir limitaciones que tu negocio no puede aceptar. Otro motivo es que, al ser un punto clave de tu negocio, es imprescindible aprender a hacerlo bien. Usar software de terceros te impide aprender a resolver problemas.

