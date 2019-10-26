+++
title = "How to get rid of scalac server exception in intellij idea - StackOverflowError"
description = ""
keywords = [
]
categories = [
]
date = "2019-10-26T08:35:31+03:30"

+++

If your scala code base in IntelliJ Idea is very large, when you run then program in Intellij Idea, you may encounter this error:

```scala
Error:scalac: Error: org.jetbrains.jps.incremental.scala.remote.ServerException
java.lang.StackOverflowError
  at scala.reflect.internal.tpe.TypeMaps$TypeMap.mapOver(TypeMaps.scala:114)
  at scala.reflect.internal.tpe.TypeMaps$AsSeenFromMap.apply(TypeMaps.scala:513)
  at scala.reflect.internal.tpe.TypeMaps$AsSeenFromMap.apply(TypeMaps.scala:483)
...
```

Increase stack size for compiler process (in Settings | Build, Execution, Deployment | Compiler | User-local build process VM options (overrides Shared options)) to e.g. -Xss4m
