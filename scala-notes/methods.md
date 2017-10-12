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


## TYPES

```scala
def add(x:Int, y:Int) = x + y
def substract(x:Double, y:Double) x - y

add(substract(10,3).toInt,substract(100,32).toInt)

add(substract(10,3).round.toInt,substract(100,32).round.toInt)

```

## RETURN TYPES

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

## UNIT

- Unit ~= void
- It is child of Any type, assignable. 
- It is an object

```scala
    def add(x:Int, y:Int):Unit = x + y 
```
returns ```()```
