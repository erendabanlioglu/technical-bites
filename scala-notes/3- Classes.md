
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


## JAVA GETTER AND SETTERS

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty var lastName:String)
// var not good!
```

```javap -p```

- firstName will have getter
- lastName will have getter and setter because it's *var*


## CONSTRUCTORS

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

## CONSTRUCTORS NAMED AND DEFAULT ARGUMENTS

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

## METHODS IN CLASSES

```scala
import scala.beans.BeanProperty

class Employee(@BeanProperty val firstName:String, 
               @BeanProperty val lastName:String,
               val title:String = "Programmer"){
     
    def fullName = s"$firstName $lastName"
    
    def changeLastName(ln:String) = new Employee(firstName, ln, lastName)
    
    def copy(firstName:String = this.firstName,  lastName:String= this.lastName, title:String:this.title){
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

## PRECONDITIONS, EXCEPTION AND EXCEPTION HANDLING

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
