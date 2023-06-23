# Day-2 Interview Questions

## What are function constructors?
Function constructors in JavaScript are a way of creating objects using a constructor function. This allows you to create multiple instances of an object with similar properties and methods.

Here's an example of how to create a function constructor in JavaScript:
```
// Define the constructor function

function Person(name, age) {

  this.name = name;

  this.age = age;

  this.greet = function() {

    console.log("Hello, my name is " + this.name + " and I am " + this.age + " years old.");

  }

}

// Create new instances of the object using the constructor function

var person1 = new Person("Alice", 25);

var person2 = new Person("Bob", 30);


// Call the greet method on each object

person1.greet(); // Output: "Hello, my name is Alice and I am 25 years old."

person2.greet(); // Output: "Hello, my name is Bob and I am 30 years old."
```

<hr>

## Explain call(), apply() and, bind() methods. Give an example of call(), apply(), bind()
call(), apply(), and bind() are all methods available in JavaScript that allow you to call a function with a specific this context and arguments.

call() and apply() are similar in that they allow you to set the this context for a function, but they differ in how they handle arguments. call() takes an argument list, while apply() takes an array of arguments.

bind() is used to create a new function with a specific this context and pre-set arguments. It does not call the function immediately but instead returns a new function that can be called later.

Here are some examples to illustrate these concepts:

call():is a function that helps you change the context of the invoking function. In layperson's terms, it helps you replace the value of this inside a function with whatever value you want.
```const person = {
  firstName: "John",
  lastName: "Doe",
  fullName: function() {
    console.log(this.firstName + " " + this.lastName);
  }
};

const person2 = {
  firstName: "Ajay",
  lastName: "Dhangar"
};


person.fullName.call(person2); // Output: Jane Doe
```

In this example, we are calling the fullName function of the person object, but we are using call() to set the this context to a new object with a different firstName and lastName. The result is a new fullName string that reflects the new context.

apply(): is very similar to the call function. The only difference is that in apply you can pass an array as an argument list.
```const numbers = [5, 10, 15, 20];

const sum = Array.prototype.reduce.apply(numbers, [(a, b) => a + b]);
console.log(sum); // 50
```

In this example, we are using apply() to call the reduce() function on the numbers array, but we are passing in the reduce() function as the this context, and we are passing in an array of arguments as the second argument to apply(). This allows us to sum up all the numbers in the array using the reduce() function.

bind(): is a function that helps you create another function that you can execute later with the new context of this that is provided.
```const person = {
  firstName: 'Ajay',
  lastName: 'Doe',
  fullName: function() {
    return this.firstName + ' ' + this.lastName;
  }
};
```
<hr>

## What is the purpose of async/await keywords?
Async/await is a feature in JavaScript that allows asynchronous code to be written in a synchronous style. This makes it easier to write and read code that deals with promises, which are a way to handle asynchronous operations in JavaScript.

The async keyword is used to define a function that returns a promise, while the await keyword is used to wait for a promise to resolve.
Here's an example:
```async function getData() {
  const response = await fetch('https://api.example.com/data');
  const data = await response.json();
  return data;
}

console.log(getData());
```
Now, let's see what happens when we don't use async and await:
```function getData() {
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
}


const getFullName = person.fullName.bind({firstName: 'Jane', lastName: 'Doe'});
console.log(getFullName()); // Jane Doe
```

In this example, we are using bind() to create a new function called getFullName that has the this context set to a new object with a different firstName and lastName. We are not calling the fullName function directly, but instead, we are calling the new getFullName function, which returns the fullName string with the new context.
<hr>

## Explain prototypes
Prototypes in JavaScript are a mechanism for object-oriented programming that allows objects to inherit properties and methods from other objects. Every object in JavaScript has a prototype, which is an object that acts as a template for the new objects created from it.

In simpler terms, a prototype is like a blueprint or a template for creating objects in JavaScript. It defines the properties and methods that an object can inherit from it.

To define a prototype in JavaScript, you can use the constructor function. Here's an example:
```function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function() {
  console.log("Hello, my name is " + this.name + " and I'm " + this.age + " years old.");
}

var person1 = new Person("Ajay", 30);
person1.greet(); // Output: Hello, my name is Ajay and I'm 30 years old.
```
<hr>

## What is prototype chain
In JavaScript, every object has a property called prototype which refers to another object. This creates a chain of objects, where each object's prototype is another object. This is called the prototype chain.

When you access a property of an object, JavaScript looks for the property in the object itself. If the property is not found, it looks in the object's prototype, then in the prototype's prototype, and so on until it either finds the property or reaches the end of the prototype chain.

Here is an example code that demonstrates the prototype chain in JavaScript:
```// Define a constructor function
function Animal(name) {
  this.name = name;
}

// Add a method to the Animal prototype
Animal.prototype.walk = function() {
  console.log(this.name + ' is walking.');
};

// Create a new instance of Animal
var cat = new Animal('Boy');

// Call the walk method on the cat instance
cat.walk(); // Output:Boy is walking.

// The walk method is not defined on the cat instance itself,
// but it is found in the Animal prototype via the prototype chain.
```
<hr>

## Give an example of inheritance using function constructor
Inheritance in JavaScript refers to the concept of creating new objects based on an existing object. The new object, also known as the child object, inherits properties and methods from the existing object, known as the parent object.

One way to implement inheritance in JavaScript is by using function constructors. A function constructor is a function that is used to create new objects. To create a child object that inherits from a parent object using function constructors, we can use the Object.create() method.

Here's an example:
```// Parent function constructor
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Child function constructor
function Employee(name, age, jobTitle) {
  Person.call(this, name, age);
  this.jobTitle = jobTitle;
}

// Inherit from parent prototype
Employee.prototype = Object.create(Person.prototype);

// Child method
Employee.prototype.introduce = function() {
  console.log("Hi, my name is " + this.name + ", and I work as a " + this.jobTitle + ".");
};

// Create a new Employee object
var employee1 = new Employee("Ajay", 22, "Software Engineer");

// Call parent and child methods
console.log(employee1.name); // output: "Ajay"
console.log(employee1.age); // output: 22
employee1.introduce(); // output: "Hi, my name is Ajay, and I work as a Software Engineer."
```