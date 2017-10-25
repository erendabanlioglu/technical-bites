## Singleton Objects

```scala
object MyObject

val a = MyObject
val b = MyObject

a == b //true
a eq b //true
```

object =~ `static`  
You can't extend from object

```scala
object MyObject {
  def foo(x: Int, y: Int) = x + y
}

MyObject.foo(5, 10) //15
```

Object can extend from class

```scala
class Employee(val firstName:String, ... )

object Knuth extends Employee("Donald", ...)

Knuth.firstName //Donald
```

Use Object if you,

- Need a singleton
- Need a factory pattern
- Need to implement pattern matching logic
- Need a utility mehod that doesn't require an instance or state
- Need default values
- Need a main method

### Main Method

```scala
object Runner {
  def main(args: Array[String]):Unit = println("Hello")
}
```

with scala-library.jar

`java -cp .;"C:\Program...\scala\lib\scala-library.jar" Runner`

Runner.scala
```scala
object Runner extends App {
   println("Hello")
}
```

## Companion Objects

Like abstract methods
Share private information between class <-> object

```scala
class SecretAgent(val name:String){
  def shoot(n:Int){
    import SecretAgent._
    decrementBullets(n)
  }
}

object SecretAgent {
  private var b:Int = 3000
  
  private def decrementBullets(count:Int){
    if(b-count <= 0) b = 0
    else b = b - count
  }
  
  def bullets = b
}

object SecretAgentRunner extends App {
  val bond = new SecretAgent("James")
  val felix = new SecretAgent("Felix")
  val jason = new SecretAgent("Jason")
  
  bond.shoot(800)
  felix.shoot(200)
  jason.shoot(150)
  
  SecretAgent.bullets //1500
}
```

```scala
class Person(val name:String, private val superHeroName:String)


object Person {
 def showMeHisIdentity(x:Person) = x.superHeroName
}

object SuperHeroRunner extends App {
  val clark = new Person( "Clark Kent", "Superman")
  Person.showMeHisIdentity(clark) //superman
}
```
Employee design factory

```scala
import java.time._

class Employee(val firstName:String, val lastName:String, val title:String, val hireDate:LocalDate)

// factory
object Employee {
 def create(firstName:String, lastName:String, title:String) =
  new Employee(firstName, lastName, title, LocalDate.Now)
}

object EmployeeDesignRunner extends App {
  val employee = new Employee.create("Kent", "Superman", "Janitor")
  employee.hiredate //<date now>
}
```

Private constructor 
Companion object have access to private constructor

```scala
import java.time._

class Employee private (val firstName:String, val lastName:String, val title:String, val hireDate:LocalDate)

// factory
object Employee {
 def create(firstName:String, lastName:String, title:String) =
  new Employee(firstName, lastName, title, LocalDate.Now)
  
  def create(firstName:String, lastName:String, title:String, hireDate:LocalDate) =
  new Employee(firstName, lastName, title, hireDate)
}

object EmployeeDesignRunner extends App {
  val employee = new Employee.create( "Kent", "Superman", "Janitor")
  employee.hiredate //<date now>
}
```

- Companion objects have the same name as the class they represent
- Companion objects must be on same file as the class they represent
- Companion objects have access to their representative class's private information
- Classes have access to companion object's private information
