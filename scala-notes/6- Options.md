## Option

Represents yes or no

             Option[T]
                | 
      Some[T]        None 

```scala
object Options extends App {
  val middleName = Some("Anthony") // Some.apply("Anthony")
  val middleName2:Option[String] = name 
  val middleName3:Some[String] = name
  
  val noMiddleName = None
  val noMiddleName2:Option[String] = noName 
  val noMiddleName3:Some[Nothing] = noName
  val noMiddleName4:None.type = noName
}
```

```scala
class Employee(firstName:String, middleName:Option[String], lastName:String) 

object Options extends App {
  // ...
  val carHoare = new Employee("Charles", Some("Anthony"), "Hoare")
  val bjarne = new Employee("Bjarne", None, "Stroustrup")
}
```

```scala
class Employee(val firstName:String, val middleName:Option[String], val lastName:String) {

  def this(firstName: String, middleName:String, lastName:String) = 
    this(firstName, Some(middleName), lastName) 
    
  def this(firstName: String, lastName:String) = 
    this(firstName, None, lastName) 
    
  def this() =  this("Unknown", "Unknowm") 
}

object Options extends App {
  // ...
  val carHoare = new Employee("Charles", "Anthony", "Hoare")
  val bjarne = new Employee("Bjarne", "Stroustrup")
  val stranger = new Employee
}
```

#Option Methods

```scala
object Options extends App {
  val middleName = Some("Anthony")
  val noMiddleName = None
  val carHoare = new Employee("Charles", "Anthony", "Hoare")
  val stranger = new Employee
  
  middleName.get //Anthony
  noMiddleName.get // error
  noMiddleName.getOrElse("No middle name") ) //No middle name
  carHoare.middleName.getOrElse("No middle name") //Anthony
  stranger.middleName.getOrElse("No middle name") //No middle name
}
```

```scala
defpeelTheMiddleName(x:Option[String]):String = {
  x match {
    case Some(name) => name
    case None => "No middle name"
  }
}

defpeelTheMiddleName(carHoare.middleName)
defpeelTheMiddleName(bjarne.middleName)
defpeelTheMiddleName(stranger.middleName)
```
