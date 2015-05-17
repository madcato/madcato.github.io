---
layout:     post
title:      "Eliminar los atributos extendidos de ficheros guardados con Textmate"
date:       2010-05-28 20:13:00
author:     "Daniel Vela"
header-img: "img/post-bg-04.jpg"
---

[Macromates](http://manual.macromates.com/en/saving_files.html)  

Para eliminar el uso de atributos extendidos del **TextMate** ejecutar la siguiente linea:

	defaults write com.macromates.textmate OakDocumentDisableFSMetaData 1  

Esto eliminará la **@** de los permisos de los ficheros que veríamos al ejecutar un `ls -al` (-rw-r--r--@).  
También evitará que al copiar estos ficheros a sistemas que no soporten atributos extendidos(como Samba), se creen ficheros de nombre ***._filename***