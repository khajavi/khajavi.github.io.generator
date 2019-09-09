---
title: "Conversion Between DTO and Entity Classes in Scala"
date: 2019-09-09T08:07:31+04:30
draft: false
tags: ["English"]
---


When you practicing DDD (Domain-Driven-Design), you need to create different bounded countexts, for example when you receive DTO object `PersonDTO`, It should be mapped to `PersonEntity`. This conversion, have lots of repetitive works to copy fields of one object to another.

In scala there is type-safa data transoformer [chimney](https://github.com/scalalandio/chimney) which can do it for you with macros and providing simple dsl for it.

[Scala-Automapper](https://github.com/bfil/scala-automapper) is another library which is similar to `chimney` but when you have some difference in fields type, you can't do it, easily like `chimney`




