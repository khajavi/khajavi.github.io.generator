+++
description = ""
keywords = [
]
categories = [
]
title = "implicit resolution"
date = "2019-11-02T11:38:24+03:30"
draft = true
+++

```scala
object PrinterExample extends App {
  
  import Printer._

  def print[T](t: T)(implicit p: Printer[T]) = p.print(t)

  println(print(5))
  println(print(List(Option(List(2,3,5)), Option(List(7)))))
}


trait Printer[T] {
  def print(t: T): String
}

object Printer {
  implicit val intPrinter: Printer[Int] = new Printer[Int] {
    def print(i: Int) = s"$i: Int"
  }

  implicit def optionPrinter[V](implicit pv: Printer[V]): Printer[Option[V]] =
    new Printer[Option[V]] {
      def print(ov: Option[V]) = ov match {
        case None => "None"
        case Some(v) => s"Option[${pv.print(v)}]"
      }
    }

  implicit def listPrinter[V](implicit pv: Printer[V]): Printer[List[V]] =
    new Printer[List[V]] {
      def print(ov: List[V]) = ov match {
        case Nil => "Nil"
        case l: List[V] => s"List[${l.map(pv.print).mkString(", ")}]"
      }
    }
}
```

