---
layout:     post
title:      "El autoengaño de los programadores"
date:       2022-04-02 01:00:00
author:     "Daniel Vela"
background: "/img/post-bg-13.jpg"
locale:       es
lang-ref:   programmer-self-delusion
---

A lo largo de mi vida profesional como programador, me he encontrado muy frecuentemente ideas que todos los compañeros defienden, pero ninguno se ha preguntado el porqué de esa idea. En ocasiones cuando alguien se me queja de que he programado algo mal, le preguntó por qué debemos hacerlo eso así: en la mayoría de los casos no he recibido respuesta, en los que sí la recibo, si seguidamente vuelvo a preguntar el porqué del porqué y entonces no hay respuesta.

Richard Dawkings acuño el termino ["meme"](https://es.wikipedia.org/wiki/Meme) para referirse a esto mismo. Un ["meme"](https://es.wikipedia.org/wiki/Meme) es una idea que todo el mundo tiene, porque se cree en su veracidad; y se cree en su veracidad, porque todo el mundo piensa así; es decir es una argumentación circular: A es B, porque B es A, y por lo tanto A es B. Esta es una falacia en la que caemos continuamente, por nuestra facilidad de confundir la causa con el efecto. 

En gran parte es motivado por la presión social, la cuál nos fuerza emocionalmente a creer y decir lo mismo
que todo el mundo cree y dice. Existe estudios psicológicos documentados donde varios participantes (todos compinchados, menos uno) se les realizaba una pregunta, a la que contestaban con una mentira muy evidente; al realizar la misma pregunta al sujeto no compinchado, -rodeado de los compinchados y habiendo oído sus contestaciones-, respondía la misma mentira evidente que el resto. 

Si esto nos ocurre con creencias evidentemente falsas, !qué haremos con ideas que no son tan fácilmente comprobables!

Os ofrezco un par de ejemplos para iluminar esta crítica.

Muchas herramientas de ["linteo"](https://es.wikipedia.org/wiki/Lint) recomiendan no crear ficheros de código con más de 1000 líneas, o algo así. ¿Qué solemos hacer los programadores cuando nos encontramos un fichero enorme? Lo separamos en dos más pequeños dividiendo el código entre los nuevos ficheros. Ni siquiera nos preguntamos cuál es la intención de dicha recomendación, la cual no es tener ficheros pequeños por que sí, en realidad tener ficheros muy grandes es un indicio (ojo, indicio, no certeza) de que la arquitectura de esa solución no está bien segregada, provocando que el código se acumule en una clase o módulo. Es decir, la solución correcta sería analizar si podemos encontrar una arquitectura mejor, más simple y clara. Pero si no la encontramos, separar las funciones en dos ficheros más pequeños, no es una solución, sino otro problema, ya que dificultamos al programador a la hora de buscar las funciones y variables dentro del código al estar separadas. 

En definitiva, los programadores sufrimos una enorme carencia de principios básicos y escalas de valores que nos permitan tomar decisiones. Sabemos que es muy importante disponer de estas herramientas para nuestro trabajo, hasta el punto que asumimos principios aparentemente buenos (como DRY, SOLID, principios Agile), sin ni siquiera analizarlos, y por ello sin encontrar sus múltiples excepciones y limitaciones. Pero no, los principios que necesitamos nos los vamos a encontrar en un manual de programación, probablemente los encontramos en otras disciplinas, como la ingeniería industrial, pero también podemos encontrarlos en los libros clásicos, libros de ética, de historia, incluso en novelas (las mejores de ellas están repletas de códigos éticos que nos pueden ayudar).
