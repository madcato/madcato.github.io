---
layout:     post
title:      "Bug de CoreData - las celdas desaparecen"
date:       2012-08-01 18:55:00
author:     "Daniel Vela"
header-img: "img/post-bg-01.jpg"
---


Muchos usuarios de LiShop se han quejado de que las listas desaparecían al crear muchos artículos.

Revisando los logs descubrí el siguiente error:

**Aug 1 18:06:38 unknown ListaCompra2[19674] \: CoreData: error: (NSFetchedResultsController) The fetched object at index 6 has an out of order section name ‘Appetizers. Objects must be sorted by section name’**

El problema era provocado porque cuando se ordenan objetos por una propiedad, esta ordenación debe coresponderse con la ordenación de las secciones del **NSFetchRequest**.

Para solucionarlo hay que poner el siguiente parámetro al construir el **NSSortDescriptor** de campos de texto. Para evitar problemas de ordenación de mayúscula / minúscula:

{% highlight objective-c %}
selector:@selector(caseInsensitiveCompare:)
{% endhighlight %}

Quedaría así:

{% highlight objective-c %}
NSSortDescriptor *sortDescriptor1 = [[NSSortDescriptor alloc] initWithKey:@"name" ascending:YES selector:@selector(caseInsensitiveCompare:)];
{% endhighlight %}