---
layout:     post
title:      "Números ‘Version’ y ‘Build’ de los proyectos Xcode"
date:       2013-03-22 12:01:00
author:     "Daniel Vela"
header-img: "img/post-bg-06.jpg"
---



Ambos códigos se encuentran en los Settings de Xcode:

![Xcode: Version and Build]({{ site.url}}/assets/tumblr_inline_mk26jyIqZ41qz4rgp.png)


Ambas se pueden modificar en el fichero de configuración *.plist* de cualquier proyecto en Xcode:

* Version: **CFBundleShortVersionString**
* Build: **CFBundleVersion**

## Diferencias

Ambos números se pueden usar de igual manera. Se puede usar el mismo identificador, pero ese no es el propósito original de Apple.

* El número de **Version** suele ser un identificador que usamos para indicar a los usuarios finales cual es la funcionalidad de una determinada versión de software: *Version 1.2.1*
* El número de **Build** suele indicar un número o código incremental para indicar que el paquete de instalación es superior a los anteriores.

## ¿Para qué se suelen usar estos dos números?

Según la documentación de Apple, estas son las características que deben cumplir los números de version y build.

**Version** suele estar compuesto por uno, dos o tres números enteros separados por punto:

1. El primero número indica la **versión mayor** de software.
2. El segundo indica una **versión menor**, o sea, algún añadido a la versión mayor.
3. El tercer número indica una **corrección**.

Por poner un ejemplo: la versión **1.1** es igual a la versión **1.0** con algúna nueva funcionalidad. La versión **2** podría ser un cambio grande de la funcionalidad de la aplicación: un cambio mayor.

Si por ejemplo, se encontraran varios fallos en la versión **1.2**, podríamos corregir dichos fallos y lanzar la versión **1.2.1** con los bugs solucionados.

**Build** suele usarse como un valor incremental que nos sirve para distinguir los paquetes de instalación independietemente de su versión.

Es muy útil cuando **hemos destribuido varias instalaciones diferentes de la misma versión**. Esto suele ocurrir frecuentemente en los equipos de testeo y al distribuir betas entre lo usuarios. Si realizamos pruebas beta de una versión determinada(pongamos la 1.3.1), tendremos que saber distinguir entre la versión distribuida esta semana, de la que se distribuyó la semana pasada. Para no confundirlas es termendamente útil usar un código **Build**.

> En tu Mac, pulsa sobre el menú de Xcode la primera opción “About Xcode” verás ambos números: el **Version** y el **Build**. Por ejemplo: Version 4.6.1 (4H512). Muchas otras apps de Apple suelen usar este convenio.

## Al subir una app al iTunes Connect

Hay dos puntos importantes a tener en cuenta al subir una nueva versión. En las pantallas del [iTunes Connect](https://itunesconnect.apple.com/)

1. Al crear la nueva versión, lo que se nos pide es indicar nuestro número de **Version**. Este debe ser igual al que hemos indicado en el proyecto. Si es diferente, nos dará un error al subir la app. 
	![iTunes Connenct: new Version]({{ site.url }}/assets/tumblr_inline_mk26le1gVo1qz4rgp.png)
2. El **Build** del proyecto debe ser superior a los enviados anteriormente. Si es igual o inferior, no se nos permitirá subir ese instalable: **hay que incrementarlo siempre antes de subir la app**. Puedes ver el número de **Build** de tus apps ya subidas en la sección *“Binary Details”* del “*Summary*” 
	![iTunes Connenct: binary details]({{ site.url }}/assets/tumblr_inline_mk26kveFyQ1qz4rgp.png)

La **Version** es un número que es mejor cambiarlo a mano cada vez que se añade funcionalidad. Sin embargo el **Build** se puede automatizar su incremento usando *scripts*.

## Mas información

* [stackoverflow: Version vs Build in XCode 4](http://stackoverflow.com/questions/6851660/version-vs-build-in-xcode-4/6965086#6965086)
* [wikipedia:Software versioning](http://en.wikipedia.org/wiki/Software_versioning)
