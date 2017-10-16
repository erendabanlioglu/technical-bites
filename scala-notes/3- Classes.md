
```scala
class Employee(firstName:String, lastName:String)
```

- public keyword not required because everythin public as default
- ```scalac Employee.scala``` -> will generate .class file
- (firstName:String, lastName:String) -> constructor 

```scala
class Employee(val firstName:String, val lastName:String)
```

```scala
val ada = new Employee("Ada", "Surname")
println(ada.firstName)
```

ada.firstName -> actually is a get method, not direct access

```scala -cp EmployeeScript.scala```
```javap -p``` you can see java byte code


## Java Getter And Setter

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty var lastName:String)
// var not good!
```

```javap -p```

- firstName will have getter
- lastName will have getter and setter because it's *var*


## Constructors

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty var lastName:String,
               val title:String){
               
    //Atypical Form   with side effect error         
    //def this(firstName:String, lastName:String) = { println("Side effect")
    //                                                 this(firstName, lastName, "programmer") }
                                                          
    //Atypical Form   with side effect        
    //def this(firstName:String, lastName:String) = { this(firstName, lastName, "programmer")
    //                                                 println("Side effect") }                                      }          
               
    //Atypical Form          
    //def this(firstName:String, lastName:String) = { this(firstName, lastName, "programmer") }
    
    //Atypical Form withouth equals         
    //def this(firstName:String, lastName:String) { this(firstName, lastName, "programmer") }
    
    //Typical Form          
    def this(firstName:String, lastName:String) = this(firstName, lastName, "programmer")
}
```
```scala
val ada = new Employee("Ada", "Surname")
println(ada.title)
```

## Constructors Named And Default Arguments

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty var lastName:String,
               val title:String = "Programmer"){
     
     // we don't need it anymore
    //def this(firstName:String, lastName:String) = this(firstName, lastName, "programmer")
}
```
```scala
val person = new Employee(lastName = "Dany", firstName = "Awesome")
```

## Methods in Classes

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty val lastName:String,
               val title:String = "Programmer"){
     
    def fullName = s"$firstName $lastName"
    
    def changeLastName(ln:String) = new Employee(firstName, ln, lastName)
    
    def copy(firstName:String = this.firstName,  lastName:String= this.lastName, title:String = this.title){
      new Employee(firstName, lastName, title)
    }
}
```

```scala
val person = new Employee(lastName = "Dany", firstName = "Awesome")
println(person.fullName)

val newPerson = person.changeLastName("new Surname")
println(newPerson.fullName)

val newPerson2 = person.copy(lastName = "new Surname 2")
println(newPerson2.fullName)
```

## Preconditions, Exception and Exception Handling

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty val lastName:String,
               val title:String = "Programmer"){
    
    // you may not to worr about null but these will not check null
    require(firstName.nonEmpty, "First name cannot be empty")
    require(lastName.nonEmpty, "Last name cannot be empty")
    
    if(title.contains("Senior") || title.contains("Junior"))
      throw new IllegalArgumentException("Title cannot contain Senior or Junior")
}
```

```scala
try {
  //new Employee("Bono", "", "Singer") 
  new Employee("Bono", "Mono", "Senior Singer")
} catch {
  case iae:IllegalArgumentException => println(iae.getMessage)
} finally { 
  // run always
}
```

## Subclasses

You can have multiple classes in same file
Inheritance must have **is-a** relationship

```scala
class Department(val name:String)

class Manager(firstName:String, lastName: String, title: String, val department:Department) 
      extends Employee(firstName, lastName, title)
  
```

```scala
val mathematics = new Department("Mathematics")

//val alan = new Manager("Alan", "Turing", "Mathematician, Logician", mathematics)

val alan:Manager = new Manager("Alan", "Turing", "Mathematician, Logician", mathematics)
val alanEmployee:Employee = alan

println(alanEmployee.firstName) 
// println(alanEmployee.department.name) //Incorrect!
  
```

```scala
def extractFirstName(e:Employee) = e.firstName
println(alan.firstName) 
println(alanEmployee.firstName) 
```

## Overriding Methods

```scala
class Department(val name:String)

class Manager(firstName:String, lastName: String, title: String, val department:Department) 
      extends Employee(firstName, lastName, title){
      
    override def fulllName = s"$firstName $lastName. ${department.name} Manager"
    
    override def copy(firstName:String = this.firstName,  lastName:String = this.lastName, title:String = this.title) = {
      new Manager(firstName, lastName, title, Department("Toys"))
    }
    
/*  Overloading   
    def copy(firstName:String = this.firstName,  lastName:String = this.lastName, title:String = this.title, department: Department = this.department) = {
      new Manager(firstName, lastName, title, department)
    } 
 */
}
  
```

## Equals, To String, Hashcode

- In AnyRef class

```scala
val ada = new Employee("Ada", "Byron", "Programmer")
val newAda = new Employee("Ada", "Byron", "Programmer")

ada == newAda // return false unless override equals
    
```
- **eq** referance equality 
- **equals** and **==** object equality

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty val lastName:String,
               val title:String = "Programmer"){
    
    ...
    
    override def equals(x:Any):Booelean = {
      if(x.isInstanceOf[Employee]) false
      else {
        val other = x.asInstanceOf[Employee]
        other.firstName ==  this.firstName &&
        other.lastName == this.lastName &&
        other.title == this.title
      }
    }
    
    override def hashCode:Int = {
      // var just mutable in this context
      var result = 19;
      result = 31 * result + firstName.hashCode;
      result = 31 * result + lastName.hashCode;
      result = 31 * result + title.hashCode;
    }
    
    override def toString = s"Employee ($firstName, $lastName, $title)"
}
```

```scala
val ada = new Employee("Ada", "Byron", "Programmer")
val newAda = new Employee("Ada", "Byron", "Programmer")

ada == newAda // return true
ada eq newAda // return false

val anotherAda = ada
ada eq anotherAda //return true

ada.hashCode == newAda //true
    
```

## Case Classes

- Automatically defined Equals, To String, Hashcode
- You can still override 

```scala
case class Department(val name:String)
```


```scala
val toys = new Department("Toys")
val toys2 = new Department("Toys")

println(toys) // prints "Department(Toys)"
toys == toys2 // true
toys.hashCode == toys2.hashCode //true
```

Have automatic pattern matching


```scala
val name = toys match {
              case Department(n) => n
              case _ => "Unknown"
            }
 println(name)
 
 // other way
 val Department(name2) = toys
 println(name2)
 
```

## Abstract Classes

- Can't be instantiated 
- Have zero or more abstract methods
- Don't have implementations
- Part of inheritance tree, any subtype can be assigned

```scala
abstract class Person{
  def firstName:String
  def lastName:String
}

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty val lastName:String,
               val title:String = "Programmer") extends Person {
               
 }

```

```scala
val ada = new Employee("Ada", "Byron", "Programmer")
val mathematics = new Department("Mathematics")
val alan:Manager = new Manager("Alan", "Turing", "Mathematician, Logician", mathematics)

//Polymorphism
val alanEmployee:Employee = alan
val alanPerson:Person = alan
val adaPeson:Person = ada
```

## Parameterized Types On Classes

```scala
case class Box[T](t:T)
```

```scala
val intBox = new Box(1)
val intBox2:Box[Int] = Box(1)
val intBox3 = Box(1):Box[3]
val intResult:Int = intBox3.t

val stringBox = new Box("Hello")
val stringBoxExplicit = Box[String]("Hello")
val managerBox = Box(new Manager("Kathy", "Sierra", "Programmer", "Department("IT"))) //Box[Manager]
val managerBox = Box[Employee](new Manager("Kathy", "Sierra", "Programmer", "Department("IT"))) //Box[Employee]

val doubleBoxBox = Box(Box(4.0)) //Box(Box[Double])
val doubleResult:Double = doubleBoxBox:t
```

```scala
case class Copule[A, B](first:A, second:B)
```

```scala
val coupleIntString = new Couple(10, "Scala")
val coupleIntString2:Couple[Int, String] = Couple(10, "Scala")
val coupleStringString = new Couple("one", "two")
val coupleDoubleInt = new Couple(30.123, 3)
val coupleStringCoupleIntDouble = Couple("hello", Couple(3, 22.2))
```

## Parameterized Methods In Classes

```scala
case class Copule[A, B](first:A, second:B){
  def swap = new Couple(second, first)
  // explicit
  // def swap: Couple[B,A] = new Couple(second, first)
}

case class Box[T](t:T){
  def coupleWith[U](u:U):Box[Couple[T,U]] = Box(Couple(t,u))
}
```

```scala
val intBox = new Box(200)
val coupeIntStringBox = intBox4.coupleWith("Scala")
val coupeIntStringBox:Box[Couple[Int,String]] = intBox4.coupleWith("Scala")

coupeIntStringBox.t.first
coupeIntStringBox.t.second
```

```scala
val employeeCouple = new Couple(new Employee("John", "McCarthy"), new Employee("Jean Claude", "Van Damme"))
employeeCouple.swap
```
