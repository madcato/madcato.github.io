---
layout:     post
title:      "Usando Ruby on Rails sin base de datos"
date:       2010-05-16 01:18:00
author:     "Daniel Vela"
header-img: "img/post-bg-04.jpg"
---

<p><a href="http://blog.veladan.org/post/45344135930/usando-ruby-on-rails-sin-base-de-datos" class="tumblr_blog">madcato</a>:</p>

<blockquote><p>Ruby On Rails se puede usar sin base de datos. Para ello hay que evitar que el gem <strong>active_record</strong> se cargue. Ya que este gem es cargado de manera automática hay que añadir esta linea al fichero <strong><em>enviroment.rb</em></strong>:</p>

{% highlight ruby %}
config.frameworks -= [:active_record]  
{% endhighlight %}

<p>Esto también se puede usar para desactivar cualquier otro gem que no necesitemos como el <strong>action_mailer</strong>.</p></blockquote>

