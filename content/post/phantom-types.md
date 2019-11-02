+++
description = ""
keywords = [
]
categories = [
]
date = "2019-11-02T09:30:54+03:30"
title = "phantom types"
draft = true

+++


```scala

object DoorExample extends App {
  import Door._
  val closedDoor: Door[Close] = Door[Close]
  val openedDoor: Door[Open] = open(closedDoor)
  val closedAgain: Door[Close] = close(closedDoor)
}


trait State
sealed trait Open extends State
sealed trait Close extends State

trait Door[S <: State]

object Door {
  def apply[S <: State] = new Door[S] {}

  def open(closedDoor: Door[Close]) = new Door[Open] {}

  def close(openedDoor: Door[Close]) = new Door[Close] {}
}
```
