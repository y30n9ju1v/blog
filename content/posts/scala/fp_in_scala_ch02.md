---
title: "[Scala] 스칼라로 배우는 함수형 프로그래밍"
date: 2022-07-24T18:04:23+09:00
categories: [
    "Scala",
]
---

# Ch02. 스칼라로 함수형 프로그래밍 시작하기

## 연습문제 2.1
~~~scala
object ex02_01 {
    def fib(n : Int) : Int = {
        @annotation.tailrec
        def go(n : Int, lhs : Int, rhs : Int) : Int = 
            if (n <= 0) lhs
            else go(n - 1, rhs, lhs + rhs)

        go(n, 0, 1)
    }

    def formatFib(n : Int) : String = {
        var msg = "The Fibbonacci of %d is %d"
        msg.format(n, fib(n))
    }

    def main(args : Array[String]) : Unit = 
        println(formatFib(0))
        println(formatFib(2))
        println(formatFib(4))
        println(formatFib(6))
        println(formatFib(10))
}
~~~

### 결과
~~~
The Fibbonacci of 0 is 0
The Fibbonacci of 2 is 1
The Fibbonacci of 4 is 3
The Fibbonacci of 6 is 8
The Fibbonacci of 10 is 55
~~~

## 연습문제 2.2
~~~scala
import scala.compiletime.ops.boolean
object ex02_02 {
    def isSorted[A](as : Array[A], ordered : (A,A) => Boolean) : Boolean = {
        @annotation.tailrec
        def go(n : Int) : Boolean = {
            if (n + 1 >= as.length) true
            else if (ordered(as(n), as(n+1)) == false) false 
            else go(n + 1)
        }

        go(0)
    }

    private def ordered(lhs: Int, rhs: Int) : Boolean = {
        if (lhs <= rhs) true
        else false
    }

    private def ordered(lhs: String, rhs: String) : Boolean = {
        if (lhs <= rhs) true
        else false
    }

    def main(args : Array[String]) : Unit = 
        var i0 = Array(0, 1, 2, 3, 4)
        var i1 = Array(0, 1, 5, 3, 4)
        println(isSorted(i0, ordered))
        println(isSorted(i1, ordered))

        var s0 = Array("apple", "book", "cook")
        var s1 = Array("book", "apple", "cook")
        println(isSorted(s0, ordered))
        println(isSorted(s1, ordered))
}
~~~

### 결과
~~~
true
false
true
false
~~~

## 연습문제 2.3
~~~scala
def curry[A, B, C](f: (A, B) => C): A => (B => C) = {
    (a : A) => ((b : B) => f(a, b))
}
~~~

## 연습문제 2.4
~~~scala
def uncurry[A, B, C](f: A => B => C) : (A, B) => C = {
    (a : A, b : B) => f(a : A)(b : B)
}
~~~

## 연습문제 2.5
~~~scala
def compose[A, B, C](f: B => C, g: A => B): A => C = {
    (a : A) => f(g(a))
}
~~~