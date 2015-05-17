---
layout:     post
title:      "Implementar una autenticación http digest con Rails"
date:       2010-05-30 03:27:00
author:     "Daniel Vela"
header-img: "img/post-bg-03.jpg"
---

Para exigir que la conexión http se autentique por **HTTP Digest** en Rails, hay que ejecutar el siguiente código:

	# ... ApplicationController class
	private  
		DUsers = {"user" => "password"}  
		def digest_authenticate  
			realm = "application"  
			authenticate_or_request_with_http_digest(realm) do |name|  
			DUsers[name]  
		end  
	end  

... y ejecutar este código antes de la invocación a nuestro método de controlador:

	 class ExampleController < ApplicationController  
	 before_filter :digest_authenticate, :only => ['index']  

	 	def index  
	 	end  
	 end  