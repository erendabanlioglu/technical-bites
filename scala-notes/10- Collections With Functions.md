## Map (function)

can be applied to List, Set, Map, Stream, String and Option

```scala
object MapFunction extends App {
  val a = List(1, 2, 3, 4, 5, 6)
  val f = (x:Int) => x + 1  
  
  // Int in Int out
  a.map(f)                  // List(2, 3, 4, 5, 6, 7)
  a.map((x:Int) => x + 1 )) // List(2, 3, 4, 5, 6, 7)
  a.map(x => x + 1 )        // List(2, 3, 4, 5, 6, 7)
  a.map( _ + 1 )            // List(2, 3, 4, 5, 6, 7)
  a.map( 1 + _ )            // List(2, 3, 4, 5, 6, 7)
  
  import scala.language.postFixOps
  a.map( 1+ )               // List(2, 3, 4, 5, 6, 7)
  
  val b = Set("Brown", "Red", "Green", "Purple", "Gray", "Yellow")
  //String in Int out
  b.map(x => x.size)        // Set(6, 4, 3, 5)   - because set can't have duplicate we have just four elements
  b.map(_.size)             // Set(6, 4, 3, 5)
  //String in Tuple out
  b.map(x => (x, x.size))   // Set((Green, 5), (Brown, 5), (Gray, 4), (Red, 3), (Yellow, 5), (Purple, 6))
  
  val fifaChamps = Map('Germany -> 4, 'Brazil -> 5, 'Italy -> 4, 'Argentina -> 2)
  fifaChamps.map(t => (Symbol.apply("Team" + t._1.name), t._2)) // Map('Team Germany -> 4, ....
   
  "Hello!".map(c => c + 1))             // Vector(73, 102, 109, ...) chars are integers
  "Hello!".map(c => (c + 1).toChart ))  // Ifmmp"
  Some(4).map(1+)                       // Some(5)
  
  val age:Option[Int] = None
  age.map(1+)                           // None
}
```

## Filter, FilterNot, Exists

```scala
object FilterFunction extends App {
  val a = 1 to 10
  a.filter(x => x % 2 == 0)     // Vector(2, 4, 6, 8, 10)
  a.filterNot(x => x % 2 == 0)  // Vector(1, 3, 5, 7, 9)
  a.exists(x => x % 2 == 0)     // true
  
  a.filter(_ % 2 == 0)     // Vector(2, 4, 6, 8, 10)
  a.filterNot(_ % 2 == 0)  // Vector(1, 3, 5, 7, 9)
  a.exists(_ % 2 == 0)     // true
  
  def filterVowels(s: String) = s.toLowerCase.filter(c => Set('a', 'e', 'i', 'o', 'u').contains(c))
  filterVowels("Orange") // oae
  
  val b = Set("Blue", "Red", "Green", "Purple", "Orange")
  b.filter(s => filterVowels(s).size > 1) //Set(Blue, Green, Purple, Orange)
  
  val m = Map(1 -> "One", 2 -> "Two", 3 -> "Three", 4 -> "Four")
  
  m.filterKeys(_ % 2 == 0)          // Map( 2 -> Two, 4 -> Four)
  Some(5).filter(_ % 2 == 0)        // None
  Some(4).filter(_ % 2 == 0)        // Some(4)
}
```

## Foreach

returns unit

```scala
object ForEach extends App {
  val a = 1 to 10
  println( a.map(x => println(x)) ) // 1 \n 2 \n .....
                                    // Vector((), (), (), ... )
                                    
  // because  println(x) Unit it returns Unit
  
  println( a.foreach(x => println(x)) ) // 1 \n 2 \n .....
                                        // ()
                                        
  a foreach println // 1 \n 2 \n .....
}
```

## FlatMap

- flatten and maps
- Can be used in List, Set, Map, Stream, String and Option

```scala
object FlatMap extends App {
  val a = List(1,2,3,4,5)
  a.map(x => List(-x, 0, x))          // List(List(-1, 0, 1), List(-2, 0, 2), ..
  a.map(x => List(-x, 0, x)).flatten  // List(-1, 0, 1, -2, 0, 2, ..
  a.flatmap(x => List(-x, 0, x))      // List(-1, 0, 1, -2, 0, 2, ..
                                    
  val b:List[List[List[Int]]] = List(List(List(1,2,3), List(4,5,6)), List(List(7,8,9), List(10,11,12)))
  b.flatMap(c => c)                   // List(List(1,2,3), List(4,5,6), List(7,8,9), List(10,11,12)) - went down 1 level
  b.flatMap(c => c).flatMap(c => c)   // List(1,2,3,4,5,6,7,8,9,10,11,12) - went down 2 level
  
  Set(2,4,10,11).flatMap(x => Set(x, x * 5)) //Set(10, 20, 2, 50, 11, 55, 4)
  
  val origMap = Map(1 -> "One", 2 -> "Two", 3 -> "Three")
  origMap.flatMap(t => Map(t._1 -> t._2, (t._1 * 100) -> (t._2 + " Hundred"))
  //Map( 1 -> One, 2 -> Two, 3 -> Three, 300 -> Three Hundred, 200 -> Two Hundred, 100 -> One Hundred)
  
  Some(4).map(x => Some(x + 19))                                      // Some(Some(23))
  Some(4).flatMap(x => Some(x + 19))                                  // Some(23)
  
  None.flatMap(x => Some(x + 19))                                     // Error!
  None.asInstanceOf[Option[Int]].flatMap(x => Some(x + 19))           // None
  Some(10).flatMap(x => None)                                         // None
  
  List(Some(4), None, Some(5), None, None, Some(10)).flatMap(x => x)  //List(4, 5, 10)
}
```
