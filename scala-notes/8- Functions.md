## Functions

- get elements (0 - 22)
- every function return only one element
- Function from 0 to 22

```scala
object Functions extends App{
  val f1:Function1[<type of param>,<type of return>] = new Function1[<type of param>,<type of return>] {
    def apply(x:<type of param>):<type of return> = x + 1
  }
}
```

```scala
object Functions extends App{
  val f1:Function1[Int,Int] = new Function1[Int, Int] {
    def apply(x:Int):Int = x + 1
  }
}
```

```scala
object Functions extends App{
  val f1:Function1[Int,Int] = new Function1[Int, Int] {
    def apply(x:Int):Int = x + 1
  }
  
  val f0:Function0[Int] = new Function0[Int] {
    def apply() = 1
  }
  
  val f2:Function0[Int, String, String] = new Function0[Int, String, String] {
    def apply(x:Int, y:String) = y + x
  }
  
  f0()
  f1(3)
  f2(4, "wow")
}
```

### Shorthand

```scala
val f1:<type of param> => <type of return> = (x:<type of param>) => x + 1 
```

```scala
object Functions extends App{
  val f1 = (x:Int) => x + 1 
  
  val f0 = () => 1
  
  val f2 = (x:Int, y:String) => y + x
}
```

### Return mutiple

We can use tuple 

```scala
object Functions extends App{
  val f3 = (x:String) => (x, x.size)
  f3("Laser") // (Laser,5)
}
```

** Carefull! New version (2.12) will use java utils **


## Methods vs Functions

```scala
object MyObject {
  val f = (x: Int) => x+1
  def g(x: Int) = x + 1
}

object YouKnowWhat extends App {
  MyObject.f.apply(4) // 5
  MyObject.f(4)       // 5
  MyObject.g(4)       // 5
}
```

- method has a context, belongs to object in this case
- function is a object it's own
- use apply for visual design to distinct function method


## Method to Function

- Using partially applied functions (underscore)
- Use an underscore to turn method paramaters into function paramaters
- If an underscore is the last characte in a method paramater, you can remove it


```scala
class Foo(x: Int){
  def bar(y: Int) = x + y
  def gym(z: Int, a:Int) = x + z + a
}

class Baz(z: Int){
  def qux(f: Int => Int) = f(z)
  def jam(f: (Int, Int) => Int) = f(z, 10)
}

object YouKnowWhat extends App {
  val x = new Foo(10)
  val f = x.bar _     // translates def to func -->  f:Int => Int = <function1>
  f.apply(20)         // 30
  f.(20)              // 30
  
  val z = new Baz(20)
  z.qux(f)            // 30
  
  // Assume f doesn't exist
  z.qux(x.bar _)      // 30
  z.qux(x.bar)        // 30   (If underscore is last you can remove)
  
  val f2 = x.gym(40, _:Int)
  z.qux(f2)           // 70
  
  val f3 = x.gym _
  z.jam(f3)           // 40
  z.jam(x.gym)        // 40
}
```

## Closures

Closures are functions that close around the environment

```scala
class Foo(x:Int){
  def bar(y:Int => Int) = y(x)
}

object Closures extends App {
  val m = 200
  val f = (x:Int) => x + m
  val foo = new Foo(100)
  foo.bar(f)                // 300
}
``` 

## Functions with Functions

Functions can take other functions in as paramaters - higher order functions
Method can take a function - higher order functions
Functions can return other functions

```scala
class FinF(x:Int){
  def bar(y:Int => Int) = y(x)
}

object FinF extends App {
  // val f:(Int, Int => Int) => Int = (x:Int, y:Int => Int) = y(x)
  val f = (x:Int, y:Int => Int) = y(x)
  
  // f(3, m = > m + 1)
  f(3, _ + 1)          //4
  //f(3, 1+)           //4   (need to import scala.language.postfixOps)
}
``` 

```scala
class FinF(x:Int){
  def bar(y:Int => Int) = y(x)
}

object FinF extends App {
  val g = (x:Int) => (y: Int) => x + y  
  g(4)(5)
  //g.apply(4).apply(5)
}
``` 
`(x:Int)`  function takes a int  
`=>`       retuns   
`(y: Int)` a function takes a int  
`=>`       returns  
           x + y  
 
## Currying

```scala
object Currying extends App {
  val g = (x:Int) => (y: Int) => x + y 
  val f = (x:Int, y:Int) => => x + y 
  
  val fc = f.curried
  val f2 = Function.uncurried(fc)
}
``` 

**fc** and **g** are same 

### Method Parameters

```scala
object CurriedParams extends App {
  def foo(x:Int, y:Int, z:Int) = x + y + z
  def bar(x:Int) (y:Int) (z:Int) = x + y + z
  def baz(x:Int, y:Int) (z:Int) = x + y + z
  
  val f = foo _       // f: (Int, Int, Int) => Int = <function3>
  val b = bar _       // b: Int => (Int => (Int => Int)) = <function1>
  val c = baz _       // c: (Int, Int) => Int => Int = <function2>
  
  val f = foo(5, _:Int, _:Int)
  val g = bar(5) _
  
  f(4, 3)         //12
  g(10)(19)       //34
 
}
``` 

Curried Paramaters are often used with implicits

## By-Name Paramaters

They can be called by block and lazily evaluated
Good for catching exceptions and cleanin up resources


```scala
object ByName extends App {
  def byValue(x:Int) (y:Int) = { println("By value"); x + y }
  def byFunction(x:Int) (y: () => Int) = { println("By function"); x + y() }
  def byName(x:Int) (y: => Int) = { println("By name"); x + y }
  
  // Eager anc clean
  val a = byValue(3) { 
      println("In call")
      19 
    }           
  // In call
  // By value
  
  // Lazy one but not clean
  val b = byFunction(3) (() => { println("In call"); 19} )  
  // By function
  // In call
  
  // Lazy and clean
  val c = byName(3) { 
    println("In call") 
    19
  }
  // By name 
  // In call
  
  
  def divideSafe(f: => Int):Option[Int] = {
    try {
      Some(f)
    } catch {
      case ae:ArithmeticException => None
    }
  }
  
  val d = divideSafely{
    val x = 10
    val y = 5
    x / y
  }
  
  println(d)
  //Some(2)
  
  val e = divideSafely{
    val x = 1000
    val y = 0
    x / y
  }
  
  println(e)
  //None
  
}
``` 
