API  
**C** - **C**lass  
**O** - companion **O**bject  
**T** - trade

## Lists
- Immutable collection
- Allow duplicates
- Index access
- Searchable
- `Nil` is a empty list 
- They can be created from companion object as well

```scala
object Lists extends App {
  val a = List(1, 2, 3, 4, 5) // List.apply
  val a2 = 1 :: 2 :: 3 :: 4 :: 5 :: Nil
  
  a.head      //1
  a.tail      //2,3,4,5
  a.init      //1,2,3,4
  a.last      //5
  
  a(4)                  // a.apply(4)
  a.min                 // 1
  a.max                 // 5
  a.isEmpty             // false
  a.nonEmpty            // true
  a.updated(3, 100)     // List(1, 2, 3, 100, 5)
  
  a.mkString(",")                 // 1,2,3,4,5
  a.mkString("**")                // 1**2**3**4**5
  a.mkString("[", "**", "]")      // 1**2**3**4**5
}
```

## Sets

- No duplicates
- No search by index
- More powerful than Lists (math.)
- Unordered
- `apply` will return `true` or `false`

```scala
object Sets extends App {
  val set = Set(1, 2, 3, 4)                     // Set(1, 2, 3, 4)
  val set2 = Set(1, 2, 3, 4, 5)                 // Set(5, 1, 2, 3, 4)
  val set3 = Set(1, 2, 3, 4, 5, 6)              // Set(5, 1, 6, 2, 3, 4)
  val set4 = Set(1, 2, 3, 4, 5, 6, 6 , 7)       // Set(5, 1, 6, 2, 7, 3, 4) 
  
  val set5 = Set(1,2)
  
  set diff set 4      // Set( )
  set4 diff set       // Set(5, 6, 7) 
  set union set3      // Set(5, 1, 6, 2, 3, 4)
  set intersect set3  // Set(1, 2, 3, 4)
  
  set ++ set3             // Set(5, 1, 6, 2, 3, 4)
  set ++ List(15, 19, 20) // Set(20, 1, 2, 3, 19, 4, 15)
  set -- set5             // Set(3, 4)
  set - 3                 // Set(1, 2, 4)
  
  set.apply(4)            // true - tests if 4 contained in the set
  set.apply(10)           // false
  set.contains(10)        // false
}
```

`union` only works with 2 Sets  
`++` and `--` has to use with collection and in this case works with any kind of traversable (any kind of list structure) 

## Maps

- Table-like collection of keys and values
- Internally collection of tuples
- Paramater as repetitave tuples (key, value)
- Symbols like Strings but guarenteed to be interned

```scala
object Maps extends App {
  val map = Map.apply((1, "One"), (2, "Two"), (3, "Three"))
  val map2 = Map((1, "One"), (2, "Two"), (3, "Three"))
  
  val t:(Int, String) = 3 -> "Three"
  println(t)                            // (3, Three)
  
  val map3 = Map(1 ->"One", 2 -> "Two"), 3 -> "Three")
  
  m3.get(1)       // some("One")
  m3.apply(1)     // "One"  - Dangerous
  m3(1)           // "One"
  m3.get(4)       //None
  m3.apply(4)     // Error
  m3(4)           // Error
  
  m3.toList           //List((1, One), (2, Two), (3, Three))
  m3.keys             // Set(1,2,3)
  m3.keySet           // Set(1,2,3)
  m3.values           // MapLike(One, Two, Three)
  m3.values.toList    // MapLike(One, Two, Three)
  m3.values.Set       // List(One, Two, Three)
  
  val s = new String("Co")
  s2 = "Co"               //interned
  s == s2                 //true
  s eq s2                 //false
  
  val co = Symbol("Co")
  co2 = 'Co               //interned
  co == co2               //true
  co eq co2               //true
  
  //Symbols are the best for maps
  
  val elements:Map[Symbol, String] = Map('Co -> "Cobalt", 'H -> Helium)
  elements.get('Co) //Cobalts
}
```

## Arrays

- Converted to primitive arrays on the JVM
- Mutable
- You can treat them like lists

```scala
object Arrays extends App {
  val a:Array[Int] = Array(1,2,3,4)
  val a:Array[Int] = Array(1,2,3,4)
    
  a.head      //1
  a.tail      //[I@547...
  a.init      //[I@212...
  a.last      //5
  
  a(4)                  // a.apply(4)
  a.min                 // 1
  a.max                 // 5
  a.isEmpty             // false
  a.nonEmpty            // true
  
  def repeatedParameterMethod(x:Int, y:String, z:Any*) = {
    println(z)
    "%d %s give you %s".format(x, y, z.mKString(", "))
  }
  
  repeatedParameterMethod(3, "eggs", "a delicious sandwich", "protein", "high cholesterol") 
  //WrappedArray(a delicious sandwich, protein, high cholesterol) 
  //3 eggs give you a delicious sandwich, protein, high cholesterol
  
   repeatedParameterMethod(3, "eggs", List("a delicious sandwich", "protein", "high cholesterol")) 
  //WrappedArray(List(a delicious sandwich, protein, high cholesterol)) 
  //3 eggs give you List(a delicious sandwich, protein, high cholesterol)
  
   repeatedParameterMethod(3, "eggs", List("a delicious sandwich", "protein", "high cholesterol"):_*) 
  //WrappedArray(List(a delicious sandwich, protein, high cholesterol)) 
  //3 eggs give you a delicious sandwich, protein, high cholesterol
}
```

## Ranges

- You can treat them with same methods as Lists
- You can use syntax sugar
- They can be created wit a factory in the Range companion object

```scala
object Ranges extends App {
  val r = (1 to 10)
  val r2 = 1 until 10       //exclude 10
  val r6 = Range(1, 10)     //exclude 10
    
  r.head                    //1
  r2.tail                   //Range(2, 3, 4, 5, 6, 7, 8, 9)
  
  val r3 = 2 to 10 by 2
  val r4 = 10 t0 2 by -2    //Range(10, 8, 6, 4, 2)
  
  val r5 = ('a' to 'z')                   //NumericRange(a, b, c, ...) 
  val r5 = ('a' to 'z') ++ ('A' to 'Z')   //Vector(a, b, c, ..., A, B, ...)
  
  val r6 = Range(1, 10)             //exclude 10
  val r7 = Range(1, 10, 2)          //step 2
  val r6 = Range.inclusive(1, 10)   //include 10
  
  for(i <- 1 to 10)
  for(i <- 1 to 10 by 2)
}
```
