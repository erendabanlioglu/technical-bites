def <method_name>(<var_name>:< type >, <var_name>:< type >):<return_type>

```scala

def add(x:Int, y:Int):Int = {
  return (x + y)
}

```
No need return type if type is constant.

No need to return keyword.

```scala

def add(x:Int, y:Int) = x + y

```

```scala

def numberStatus(a:Int) = {
  if(a<10) "Less than 10"
  else "10 or greater"
}

```


## Types

```scala
def add(x:Int, y:Int) = x + y
def substract(x:Double, y:Double) x - y

add(substract(10,3).toInt,substract(100,32).toInt)

add(substract(10,3).round.toInt,substract(100,32).round.toInt)

```

## Return Types

```
            scala.Any
     ________|     |_________
     |                      | 
scala.AnyVal        scala.AnyRef
```

Code
```scala
def add(x:Int, y:Int) = {
  if(x > 10) (x + y).toString
  else x + y
})

```
Interpreation
```scala
add: (x: Int, y: Int)Any
```

## Unit

- Unit ~= void
- It is child of Any type, assignable. 
- It is an object

```scala
def add(x:Int, y:Int):Unit = x + y 
```
returns ```()```

## Recursion

Return type must be declared

```scala
def factorial(n:BigInt):BigInt = {
  if(n ==0  || n == 1) 1
  else n * factorial(n - 1)
} 
```

it will have stack overflow error on big big numbers. To fix see below

### Tail Optimized

tailrec = tail recursive 

```scala
import scala.annotation.tailrec

@tailrec
def factorial(n:BigInt, acc:BigInt):BigInt = {
  if(n ==0  || n == 1) acc
  else factorial(n - 1, acc * n)
} 

def getFactorial(n:Int) = factorial(n, 1)
```


## Methods In Methods

```scala
import scala.annotation.tailrec

def getFactorial(n:Int) = {
   @tailrec
   def factorial(n:BigInt, acc:BigInt):BigInt = {
      if(n ==0  || n == 1) acc
      else factorial(n - 1, acc * n)
    }
    factorial(n, 1)
}
```

## Last Method Name Bender

```scala
def `Summation of` (x:Int, y:Int) = x +y

`Summation of`(x,y)

```

```scala
def areWeHere_? = true
```

this is a method, returns boolean

## Operator Overloading

```scala
def +(x:Int, y:Int) = x + y
```

## Method Overloading

```scala
def addNum(x:Int) = x + 1
def addNum(y:Double) = y + 30.0
def addNum(z:String) = z + 19

addNum(30)
addNum(40.0)
addNum("Hello")
```

## Arguments

#### Named Arguments

```scala
def processNumbers(b:Boolean, x:Int,  y:Int) = if(b) x else y

processNumbers(true, 10, 41) //10
processNumbers(x = 10, y = 41, b = true) //10
```

#### Default Arguments

```scala
def processNumbers(b:Boolean = true, x:Int,  y:Int) = if(b) x else y

processNumbers(10, 41) //error
processNumbers(x = 10, y = 41) //10
```

## IS/AS Instance Of

```scala
3.isInstanceOf[Int] //true
"3".isInstanceOf[String] //true
"3".isInstanceOf[CharSequence] //true
```

![alt text](https://github.com/erendabanlioglu/technical-bites/blob/master/scala-notes/files/string.PNG "Logo Title Text 1")

```scala
val g:Any = "ice ice baby"
val h:String = g //type mismatch. need casting
val h:String = g.asInstanceOf[String]
```

```scala
def decide(x:Any) = if (x.isInstanceOf[Int]) x.asInstanceOf[Int] + 1 else -1

decide(4) //5
decide("Hello") //-1
```
## Parameterized Types On Methods

```scala
def decide(b:Boolean, x:Any, y:Any):Any = if (b) x else y

decide(true, "A", "B") //A (Any)
decide(false, 3, 10) //10 (Any)
decide(true, c, d) //c (Any)

var result = decide(true, 'c', 'd') // result in Any type
if(result.isInstanceOf[Char]){
  val charResult = result.asInstanceOf[Char]
}
```

maybe make it better?

```scala
def decide[T](b:Boolean, x:T, y:T):T = if (b) x else y

decide(true, "A", "B") //A (String)
decide(false, 3, 10) //10 (Int)
decide(true, 'c', 'd') //c (Char)
decide(true, 3, "G") //3.0 (Any)
decide(true, 40, 'c') //40 (Int)

```

behind the scene characters are number, due to promotion it will convert to int so 'c'acts like int
