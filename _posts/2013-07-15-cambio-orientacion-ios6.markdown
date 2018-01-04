---
layout:     post
title:      "Cambio de orientación en iOS 6"
date:       2013-07-15 11:56:00
author:     "Daniel Vela"
header-img: "img/post-bg-05.jpg"
---

Con iOS 6 cambiaron la manera de controlar la orientación de las vistas. Ahora se pregunta al controlador raiz de UIWindow.

Cuando el controlador raíz es un objeto de las clases UINavigationController o UITabBarController, tenemos un problema. Estos controladores siempre responden afirmativamente al cambio de orientación.

Para solucionar este problema podemos usar el siguiente código:

{% highlight objc %}
#pragma mark - UITabBarController

@implementation UITabBarController (Rotation_IOS6)

-(BOOL)shouldAutorotate
{
    return [[self.viewControllers lastObject] shouldAutorotate];
}

-(NSUInteger)supportedInterfaceOrientations
{
    return [[self.viewControllers lastObject] supportedInterfaceOrientations];
}

- (UIInterfaceOrientation)preferredInterfaceOrientationForPresentation
{
    return [[self.viewControllers lastObject] preferredInterfaceOrientationForPresentation];
}

@end

#pragma mark - UINAviagationController

@implementation UINavigationController (Rotation_IOS6)

-(BOOL)shouldAutorotate
{
    return [[self.viewControllers lastObject] shouldAutorotate];
}

-(NSUInteger)supportedInterfaceOrientations
{
    return [[self.viewControllers lastObject] supportedInterfaceOrientations];
}

- (UIInterfaceOrientation)preferredInterfaceOrientationForPresentation
{
    return [[self.viewControllers lastObject] preferredInterfaceOrientationForPresentation];
}

@end

{% endhighlight %}