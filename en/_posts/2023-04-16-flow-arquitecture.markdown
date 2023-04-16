---
layout:     post
title:      "Unidirectional flow architectures for iOS"
subtitle:   "What are flow architectures and examples."
date:       2023-04-21 13:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-02.jpg"
locale:     en
lang-ref:   flow-arquitecture
---

## What are unidirectional flow architectures?
Flow architectures are an interesting way to think about software design, and have gained popularity in recent years due to their ability to simplify the development process and keep applications scalable. In this post, we will explore some examples of flow architectures, their advantages, and how they are applied in the real world.

It is important to understand the idea behind flow architectures. Instead of thinking of software as a collection of components, **flow architectures view it as a continuous stream of data**. This means that the software is organized around data flows and how it moves through the application.

The data flow can be controlled by a "controller" that ensures that the data gets to where it needs to go. Instead of having multiple components talking to each other, all parts of the application connect to the controller, simplifying the design.

One of the most popular examples of a flow architecture is the event architecture. This architecture is very popular in system programming and mobile application development. The idea behind this architecture is simple: **events are used to communicate information between different parts of the application**.

In this model, the application is divided into small parts called "events". These events are sent through a central event bus that distributes them to the different components of the application. The components can be services, databases, messaging services, **and the views that initiate the events; making a complete journey in a single direction**. Each component receives the events that interest it and processes them according to its needs.

This animation from the Suas project shows how the one-way data flow architecture works.

![Unidirectional data flow architecture](https://camo.githubusercontent.com/20f9063b591f63cf779535868fdd7ca01a09dc2ac38c43d369cfc51dd5125364/687474703a2f2f692e696d6775722e636f6d2f453743783274662e676966)

## Examples of flow architectures applied to mobile programming
These are just a few libraries that use flow architecture.

- [Suas](https://github.com/madcato/Suas-iOS) is an implementation of the Flux one-way dataflow architecture for iOS. It has a good explanatory animation of what this type of architecture is. This project seems discontinued, it originally belonged to ZenDesk. It's a shame because it had an excellent logging system.

- [The Composable Architecture](https://github.com/pointfreeco/swift-composable-architecture). This library allows you to build applications in a consistent and understandable way, through composition, testing and ease of use. It can be used with SwiftUI or UIKit and on any platform that Swift supports.

- [Reswift: Unidirectional Data Flow in Swift - Inspired by Redux](https://github.com/ReSwift/ReSwift). ReSwift is like a Redux implementation of the one-way dataflow architecture for Swift.

## Other resources
- [Awesome iOS architecture](https://github.com/onmyway133/awesome-ios-architecture#swiftui). This is an excelent resource contaning a list of many other libraries that use iOS architectures, and articles about architecture.