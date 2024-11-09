# Object Oriented JavaScript:
-----------------------------------------------------------

Object-oriented programming (OOP) in JavaScript is a paradigm that allows you to create objects that have both data and behavior associated with them. While JavaScript is a prototype-based language rather than a class-based one like Java or C++, it still supports many object-oriented principles.

Here's a brief overview of how you can implement OOP concepts in JavaScript:

1. **Objects**: In JavaScript, everything is an object (or can be treated as one). You can create objects using object literals `{}`, constructor functions, or ES6 classes.

   ```javascript
   // Using object literal
   let obj = {
       property1: value1,
       property2: value2,
       method() {
           // method definition
       }
   };

   // Using constructor function
   function MyClass(property1, property2) {
       this.property1 = property1;
       this.property2 = property2;
       this.method = function() {
           // method definition
       };
   }
   let obj = new MyClass(value1, value2);

   // Using ES6 class
   class MyClass {
       constructor(property1, property2) {
           this.property1 = property1;
           this.property2 = property2;
       }
       method() {
           // method definition
       }
   }
   let obj = new MyClass(value1, value2);
   ```

2. **Inheritance**: JavaScript supports inheritance through prototype chaining. You can use the `prototype` property or `class` syntax to achieve inheritance.

   ```javascript
   // Using prototype
   function Parent() {}
   Parent.prototype.method = function() {
       // method definition
   };

   function Child() {}
   Child.prototype = Object.create(Parent.prototype);
   Child.prototype.constructor = Child;

   // Using class
   class Parent {
       method() {
           // method definition
       }
   }

   class Child extends Parent {
       // additional methods
   }
   ```

3. **Encapsulation**: JavaScript doesn't have built-in access modifiers like private or protected, but you can achieve encapsulation through closures or naming conventions.

   ```javascript
   function MyClass() {
       let privateVariable = 'private';

       this.getPrivateVariable = function() {
           return privateVariable;
       };
   }

   let obj = new MyClass();
   console.log(obj.getPrivateVariable()); // Output: private
   ```

4. **Polymorphism**: JavaScript supports polymorphism naturally because of its dynamic typing and duck typing nature.

   ```javascript
   class Animal {
       makeSound() {
           console.log('Some generic sound');
       }
   }

   class Dog extends Animal {
       makeSound() {
           console.log('Woof!');
       }
   }

   class Cat extends Animal {
       makeSound() {
           console.log('Meow!');
       }
   }

   let dog = new Dog();
   let cat = new Cat();

   dog.makeSound(); // Output: Woof!
   cat.makeSound(); // Output: Meow!
   ```

These are just some basic concepts of object-oriented programming in JavaScript. As you dive deeper, you'll encounter more advanced topics like mixins, composition, and design patterns which can further enhance your understanding and use of OOP in JavaScript.
