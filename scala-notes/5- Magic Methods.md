## Apply

```scala
class Foo(x:Int) {
  def bar(y:Int) = x + y
}

object MagicApply extends App {
  var foo = new Foo(10)
  foo.bar(20) //30
}
```
if method named **apply** no need to invoke directly

```scala
class Foo(x:Int) {
  def apply(y:Int) = x + y
}

object MagicApply extends App {
  var foo = new Foo(10)
  foo(20) //30
}
```


```scala
import java.time._

class Employee private (val firstName:String, val lastName:String, val title:String, val hireDate:LocalDate)

// factory
object Employee {
  def apply(firstName:String, lastName:String, title:String) =
    new Employee(firstName, lastName, title, LocalDate.Now)
  
  def apply(firstName:String, lastName:String, title:String, hireDate:LocalDate) =
    new Employee(firstName, lastName, title, hireDate)
}

object EmployeeDesignRunner extends App {
  val employee = Employee("Kent", "Superman", "Janitor")
}
```


```scala
case class Department(name:String)

object EmployeeDesignRunner extends App {
  val employee = Employee("Kent", "Superman", "Janitor")
  
  val department = Department.apply("Sports)
  val department2 = Department("Sports)
}
```

Apply can be object or class

## Infix Operators

It allows method to be invoked without dot or paranthesis  
If there are more than one param you need paranthesis

```scala
  class Foo(x:Int){
    def bar(y: Int) = x + y
    def baz(a:Int, b:Int) = x + a + b
    def qux(y:Int) = new Foo(x + y)
  }
  
  object InfixOperatorRunner{
    val foo - new Foo(10)
    foo.bar(5) //15
    foo bar 5 //15
    
    foo.baz(10, 14) //34
    foo baz (10, 14) //34
    
    foo bar 4 + 19
    foo qux 4 qux 10 qux 19 qux (100 + 19) bar 40 + 300
  }
  
```

## Right Associative Colons 

```scala
  object RightAssociativeColons extends App{
    class Foo(x:Int){
        def ~(y: Int) = x + y
      }
      
      val foo = new Foo(10)
      foo.~:(5) //15
      5 ~: foo //15 - Right Associative Colon
  }
  
```
