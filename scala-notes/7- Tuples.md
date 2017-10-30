## Tuples

It's a just container
Typed
Usefull for returning multiple items

```scala

object Tuples extends App {
  val t = (1, "Cool", 402.00)
  t._1 //first (like haskell)
  t._2
  t._3
  
  val t1:(Int,String, Double) = t // no need to declare normally
  val t2:Tuple3[Int,String, Double] = t // it goes up to Tuple22
}

```

```scala
case class Department (name: String)
val u = ("4", Department("QA")
u //(4, Department(QA))
val u2 = u.swap
u2 //(Department(QA), 4)

```

Just Tuple2 has a swap method!
