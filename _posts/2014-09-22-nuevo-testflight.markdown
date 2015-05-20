---
layout:     post
title:      "Nuevo TestFlight"
date:       2014-09-22 15:41:00
author:     "Daniel Vela"
header-img: "img/post-bg-02.jpg"
---

Apple compró TestFlightApp. Ahora lo acaba de integrar con su servicio “iTunes Connect”. Han eliminado la funcionalidad del SDK y no consigo ver donde descargar los “Crash Logs”: sería extraño que Apple no haya incluido esta funcionalidad.

Un punto muy positivo que he encontrado es que en este nuevo TestFlight se puede enviar la versión de tu App firmada con un certificado de tipo App Store. Es decir, el mismo archivo .ipa que envías a Apple para que lo publique, es el que se usa para que los beta testers se instalen la app. No es necesario crear una versión Ad Hoc y otra App Store.

Ahora los provisioning Ad Hoc solo serán necesarios si quieres enviar el .ipa por correo a alguien para que se lo instale con el iTunes.

Algo que me queda por probar es si se puede enviar una invitación para que testea tu app a alguien cuyo iPhone no esté en la lista de dispositivos de prueba del “Povissioning Portal”.