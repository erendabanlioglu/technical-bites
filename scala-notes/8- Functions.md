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

// TO DO
