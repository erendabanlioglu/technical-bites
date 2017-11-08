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

## Forach

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
