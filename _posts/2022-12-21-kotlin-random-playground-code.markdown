---
layout: post
title:  Kotlin Random Playground Code
description:
date:   2022-12-21 00:31:46.882708 -0500
author: sdemian
image:  '/images/2022-12-21-kotlin-random-playground-code.jpg'
tags:   [kotlin, technology]
tags_color: '#477690'
featured: true
---
Creating Kafka consumer using Kotlin is fun - at least they say so, why not to first play with Kotlin idiom and code.

> Kotlin Random Playground Code

Trying different code snippets with Kotlin version 1.7.21

{% highlight kotlin linenos %}
open class Shape

class Rectangle(var height: Double, var length: Double): Shape() {
  var perimeter = (height + length) * 2
}

fun maxOf(a: Int, b: Int): Int {
  if (a > b) return a else return b
}

fun describe(obj: Any): String =
  when (obj) {
    1           -> "One"
    "Hello"     -> "Greeting"
    is Long     -> "Long"
    !is String  -> "Not a string"
    else        -> "Unknown"
  }

fun parseInt(str: String): Int? {
  return str.toIntOrNull()
}

fun printProduct(arg1: String, arg2: String) {
  val x = parseInt(arg1)
  var y = parseInt(arg2)
  
  if (x != null && y != null) {
    println(x * y)
  } else {
    println("$arg1 or $arg2 is not a number")
  }
}

fun main() {
  val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
  
  fruits
    .filter { it.startsWith("a") }
    .sortedBy { it }
    .map { it.uppercase() }
    .forEach { println(it) }
      
  printProduct("6", "7")
  printProduct("a", "7")
  printProduct("a", "b")
}
{% endhighlight %}
