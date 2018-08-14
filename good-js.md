
- Object.defineProperty provide protected/writable property.

## Prototype

```javascript
function personFactory(firstName, lastName){
  return {
    firstName,
    lastName,
    greet: function(person) {
      return "Hello, " + person.firstName;
    }
  }
}
```

evertime new person object created greet function object will be created and use too much memory.

let johnDoe = personFactory("John", "Doe");
let janeDoe = personFactory("Jane", "Doe");

johnDoe.greet === janeDoe.greet --> false

```javascript
let personFactory = (function(firstName, lastName){
  let personPrototype = {
    greet: function(person) {
        return "Hello, " + person.firstName;
      }
  }

  return function(firstName, lastName) {
    let person = Object.create(personPrototype, {
      firstName: {writable: false, value: firstName},
      lastName: {writable: false, value: firstName},
    })
  }
})();
```

We use immediatly called method to don't make `personPrototype` global.

let johnDoe = personFactory("John", "Doe");
let janeDoe = personFactory("Jane", "Doe");

johnDoe.greet === janeDoe.greet --> true


Use prototype approach for objects keys which are not modified.

## Privacy

Symbol (easy, not 100% prviacy), WeakMap (100% privacy, hard)

```javascript
let Person = (function(){
  const firstNameSymbol = Symbol();
  const lastNameSymbol = Symbol();
  
  class Person {
    constructor(firstName, lastName){
      this[firstNameSymbol] = firstName;
      this[lastNameSymbol] = lastName;
    }

    static greet(person) {
      return "Hello, " + person[firstNameSymbol];
    }

    get fullName() {
      return this[firstNameSymbol] + " " + this[lastNameSymbol];
    }

    get firstName() {
      return this[firstNameSymbol];
    }

    get lastName() {
      return this[lastNameSymbol];
    }
  }
  
  return Person;
})();

let johnDoe = new Person("John", "Doe");
```

You can still access to variable by symbols and you can retrieve all symbols in the objecy. ( Object.getOwnPropertySymbols(johnDoe) ).

```javascript
let Person = (function(){
  const privateData = new WeakMap();
  
  class Person {
    constructor(firstName, lastName){
      privateData.set(this, {firstName, lastName});
    }

    static greet(person) {
      return "Hello, " + privateData.get(person).firstName;
    }

    get fullName() {
      return privateData.get(this).firstName + " " +  privateData.get(this).lastName;
    }

    get firstName() {
      return rivateData.get(this).firstName;
    }

    get lastName() {
      return privateData.get(this).lastName;
    }
  }
  
  return Person;
})();
```

## Immutable

```javascript
function createPoint(x, y) {
  return Object.freeze({
    x,
    y
  });
}

let point = createPonit(1, 2); 
point.x = 5 // error
```

```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    
    Object.freeze(this);
  }
} 


class ThreeDPoint extends Point { 
  constructor(x, y) {
    super(x, y);
    this.z = z;
   
  }
}

let point = createPonit(1, 2);  //ok
let point3d = ThreeeDPoint(1, 2, 3) //not ok

```
Conditioning:

```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    
    if(this.constructor === Point){
      Object.freeze(this);
    }
  }
} 


class ThreeDPoint extends Point { 
  constructor(x, y) {
    super(x, y);
    this.z = z;
    
    if(this.constructor === ThreeDPoint){
      Object.freeze(this);
    }
  }
}

let point3d = ThreeeDPoint(1, 2, 3) //ok
point3d.z = 14; //error

```

## THIS

the value of this determined when the function executed.
