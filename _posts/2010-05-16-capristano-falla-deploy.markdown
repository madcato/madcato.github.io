---
layout:     post
title:      "Capristano falla al realizar deploy"
date:       2010-05-16 01:32:00
author:     "Daniel Vela"
header-img: "img/post-bg-05.jpg"
---

Son muchos los fallos que nos podemos encontrar al realizar un deploy con Capristano.  
Voy a comentar uno de ellos. Este fallo se produce cuando al ejecutar un cap deploy nos devuelve el siguiente error:

	executing "svn checkout -q -r4 svn+ssh://root@[server_name]/root/[...] /var/www/html/[...]/releases/20100515165617 && (echo 4 > /var/www/html/[...]/releases/20100515165617/REVISION)"  
	servers: ["[server_name]"]  
	[server_name] executing command  
	** [[server_name] :: err] Address [ip.ip.ip.ip] maps to [server_name], but this does not map back to the address - POSSIBLE BREAK-IN ATTEMPT!  
	** [[server_name] :: err] Permission denied, please try again.  
	** [[server_name] :: err] Permission denied, please try again.  
	** [[server_name] :: err] Permission denied (publickey,gssapi-with-mic,password).  
	** [[server_name] :: err] svn: Connection closed unexpectedly  
	command finished[/shell]  

Sin embargo, si ejecutamos este código directamente en el servidor,...  

svn+ssh://root@[server_name]/root/[...] /var/www/html/[...]/releases/20100515165617 && (echo 4 > /var/www/html/[...]/releases/20100515165617/REVISION)[/shell]
..., funciona perfectamente.

La causa de este error es que **capristano** espera que la autenticación del protocolo ssh funcione automáticamente usando la clave pública. Pero por algún motivo que desconozco, esta autenticación falla.

Para solucionar este problema podemos usar el siguiente método:

En el fichero ***Capfile*** de nuestro proyecto Rails incluir la siguiente linea.

	default_run_options[:pty] = true  

Al aplicar este cambio y ejecutar el **cap deploy** capristano nos pedirá que introduzcamos el pasword de nuestra conexión ssh con el servidor. No es una solución bonita, pero funciona.