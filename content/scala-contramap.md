+++
description = ""
draft = false
keywords = [
]
categories = [
]
date = "2019-08-10T19:29:06+04:30"
title = "Scala Contramap"
tags = ["English"]

+++

Contramap function have the following definition:

```scala
def contramap[A, B](fa: F[A])(f: B => A): F[B]
```

For example `scala.math.Ordering` have `by` function that is contramap, we can create Complicated orderings by use of Simple Orderings.

```scala
def by[T, S](f: T => S)(implicit ord: Ordering[S]): Ordering[T]
```

Create Ordering for type Money with `by` contramap

```scala
case class Money(amount: Int)

import scala.math.Ordered._

implicit val moneyOrdering: Ordering[Money] = Ordering.by(_.amount)

Money(300) < Money(200)
```

