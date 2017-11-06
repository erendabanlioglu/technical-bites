API  
**C** **C**lass  
**O** companion **O**bject
**T** trade

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
