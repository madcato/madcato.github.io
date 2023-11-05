---
layout:     post
title:      "SOLID Principles"
subtitle:   "What are SOLID principles?"
date:       2023-11-05 06:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-04.jpg"
locale:     en
lang-ref:   solid-principles
---

# SOLID

The SOLID principles are commonly used to guide architectural decisions in software development. They are five rules designed to encourage clean and extensible object-oriented code, ensuring stable behavior without the need to modify existing code.

The SOLID principles are:

1.	**Single Responsibility**: Each class or function should have a single responsibility. If a class handles multiple tasks, it’s advisable to split it into simpler classes with unique responsibilities. The same applies to functions: if a function has too many parameters or performs numerous operations, it should be divided into smaller, more specific functions.
Properly naming variables, classes, and functions to reflect their exclusive responsibility is crucial.
2.	**Open/Closed**: Classes should be open for extension but closed for modification. Instead of changing the behavior of an existing class, it’s better to create a new one that extends it.
Modifying a class often contravenes the first SOLID principle. Designing classes that can be extended without being modified is a way to avoid this problem.
3.	**Liskov Substitution**: Instances of derived classes should be able to replace those of their base classes. This means that specializations should maintain the behaviors of the base class, adjusting details to comply with the base class’s contract.
4.	**Interface Segregation**: It’s preferable to have multiple small interfaces rather than one large one. This principle is similar to Single Responsibility but applied to interfaces.
5.	**Dependency Inversion**: One should depend on abstractions, not concrete implementations. This means that our code should interact with interfaces, not specific implementations, often achieved through dependency injection.

## Conclusions

Although these principles are associated with object-oriented programming, they are not exclusive to it. They help to improve code cohesion and prevent excessive dependencies between classes, allowing each part of the code to know only what it needs to function correctly.
