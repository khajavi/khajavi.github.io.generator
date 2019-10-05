+++
categories = [
]
date = "2019-08-20T13:48:13+04:30"
title = "Scala Intramap"
description = ""
keywords = [
]

+++
Intramap have following definition:

```scala
def imap[A, B](fa: F[A])(f: A => B)(g: B => A): F[B]
```

So when you have Funtor[A] and you want to create new Functor[B] which is invariant with Functor[A] you can use `imap` method.

In following example, You I've wrote Codec for `Person` type, by using `String` Codec.

```scala
trait Codec[A] {
  self =>
  def encode(value: A): String

  def decode(value: String): A

  def imap[B](dec: A => B, enc: B => A): Codec[B] = new Codec[B] {
    override def encode(value: B): String =
      self.encode(enc(value))

    override def decode(value: String): B =
      dec(self.decode(value))
  }
}

def encode[A](value: A)(implicit c: Codec[A]): String = c.encode(value)

def decode[A](value: String)(implicit c: Codec[A]): A = c.decode(value)


object CodecImplicits {


  implicit val stringCodec: Codec[String] = new Codec[String] {
    override def encode(value: String): String = value

    override def decode(value: String): String = value
  }

  implicit val intCodec: Codec[Int] = stringCodec.imap(
    _.toInt, _.toString
  )
}

import CodecImplicits._

case class Person(name: String, age: Int)

implicit val personCodec: Codec[Person] = stringCodec.imap[Person](
  str => {
    val lines = str.split(',')
    Person(decode[String](lines(0)), decode[Int](lines(1)))
  },
  person => s"${person.name},${person.age}"
)

val ali: String = encode[Person](Person("Ali", 25))
val mohammad: Person = decode[Person]("Mohammad,23")

println(ali)
println(mohammad)
```

Result: 

```
Ali,25
Person(Mohammad,23)
```
