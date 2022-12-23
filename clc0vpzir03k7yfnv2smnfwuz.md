# Difference between types and interfaces in Typescript

It is common for beginners to get confused about **types** and **interfaces** in TypeScript, especially if they are new to typed programming languages. It is straightforward to start with TypeScript, but sometimes we need to think more about our best use case. In this case, types or interfaces?

## Types and type aliases
Before I explain the difference between types and interfaces, we need to make something clear.

In TypeScript, we have a lot of basic types, such as string, boolean, and number. Also, TypeScript allows you to create a new **name** for a **type** using the type keyword called a "type alias." This can be useful for building more expressive and self-explanatory code or making it easier to refer to complex types.

Here is an example of using a type alias:

```ts
type StringOrNumber = string | number;
```
In this example **StringOrNumber** is a new name for a type, not a new type. We use the type keyword to create a new **type alias**. That’s why some people might get confused and think that it’s creating a new type when they’re only creating a new name for a type. So when you see someone talking about the difference between types and interfaces, like in this post, you can bet that person is talking about type aliases and interfaces.

## Types vs. interfaces
A type in TypeScript is a way of specifying the shape of a value. It can be used to describe the expected structure of an object, the expected return type of a function, or the type of a variable. Types can be simple, such as numbers or strings, or they can be complex, such as objects or arrays.

An interface, on the other hand, is a way of describing the structure of an object. It is used to define a set of properties that an object should have, along with their types. An interface can be implemented by a class, which means that the class must have all of the properties and methods defined in the interface.

One way to think about the difference between types and interfaces is that a type is a way of describing the shape of a value, while an interface is a way of describing the shape of an object.

## Declaration merging
One thing that interfaces can implement but types can't is declaration merging. Declaration merging is a feature in TypeScript that allows you to combine multiple interfaces of the same name into a single definition.

Here's an example of how declaration merging works:

```ts
interface IPerson {
  name: string;
  age: number;
}

interface IPerson {
  address: string;
}

// The two declarations of IPerson are merged into a single definition:
// interface IPerson {
//   name: string;
//   age: number;
//   address: string;
// }
```
In this example, the two declarations of IPerson are merged into a single **definition** that includes both the **name** and **age** properties from the first interface and the **address** property from the second interface. **Note** that trying do the same thing with **types** will throw us en error.

## Extending interfaces
In addition to declaration merging, an interface can also be extended with classes, which is impossible with types. This is excellent content that helps a lot in OOPs. We can also create classes executing interfaces.

To **extend** an interface, you can use the **extends** keyword followed by the name of the interface you want to extend. For example:

```ts
interface Shape {
  color: string;
}

interface Square extends Shape {
  sideLength: number;
}
```
In this example, the **Square** interface extends the **Shape** interface, which means that any object that implements the **Square** interface must have both a **color** property and a **sideLength** property.

To implement an interface in a class, you can use the **implements** keyword followed by the name of the interface. For example:

```ts
class Square implements Shape {
  color: string;
  sideLength: number;

  constructor(color: string, sideLength: number) {
    this.color = color;
    this.sideLength = sideLength;
  }
}
```
In this example, the Square class implements the Shape interface, which means that it must have a color property. The class also has a sideLength property, which is required by the Square interface.

It is important to note that when you implement an interface in a class, you must include all of the properties and methods defined in the interface. If you forget to include any of them, you will get a compile-time error.

## Type intersection
In TypeScript, the intersection type combines multiple types into one. It allows you to specify that a value can have multiple types at the same time.

Here's an example of how you might use an intersection type:
```ts
type HasName = { name: string };
type HasAge = { age: number };

type Person = HasName & HasAge;

const person: Person = {
  name: "John",
  age: 30
};
```
In this example, the **Person** type is the intersection of the **HasName** and **HasAge** types, which means that it has property of both type HasName and HasAge. The **person** variable is of type **Person** and can have values for both the **HasName** and **HasAge** properties.

One good thing is that you can also create new intersection types combining multiple interfaces. However, you cannot create an interface combining two types.

Here is an example:

```ts
interface A {
  a: number;
}

interface B {
  b: string;
}

type AandB = A & B; //Correct

/*interface AandB {
   A & B
}
This will throw an error as it is not possible to intersect types with interfaces.
*/

let ab: AandB = {
  a: 42,
  b: 'hello'
};
```

## Tuples
In TypeScript, a tuple is a data type that represents an ordered list of elements with a fixed number of elements. Each element in a tuple can be of a different type.

Here's an example of a tuple in TypeScript:

```ts
let tuple: [string, number];

tuple = ["hello", 10]; // valid
tuple = [10, "hello"]; // invalid
```
In the example above, the tuple has two elements: a string and a number. The first element must be a string and the second element must be a number. Trying to assign an array with the elements in the wrong order will result in a type error.

Tuples genereally used with types but if you want to you can also use tuples with interfaces.

For example:

```ts
interface Tuple {
  0: string;
  1: number;
}

let tuple: Tuple;

tuple = ["hello", 10]; // valid
tuple = [10, "hello"]; // invalid
```
In this example, the interface Tuple defines the structure of the tuple, with the first element being a string and the second element being a number. This allows you to use the interface to type the tuple variable and ensure that it has the correct structure.

## What should I use?
The choice between using types or interfaces in TypeScript depends on your specific needs and the context in which you are using them. Here are some general guidelines to help you decide which one to use:

- Use types when you want to describe the structure of a value in a general way. This could include basic types like strings and numbers, as well as more complex types like arrays and objects. Types can be used to specify the type of a variable, function parameter, or return value.

---

- Use interfaces when you want to describe the structure of an object in a more specific and rigid way. An interface defines a set of properties and methods that an object should have, and any object that implements that interface is expected to have those properties and methods. Interfaces are a good choice when you want to enforce a certain structure on objects in your code.

---

- Use both types and interfaces when you want to combine the flexibility of types with the rigidity of interfaces. For example, you might use a type to describe the general structure of an object, and then use an interface to describe a more specific version of that object that has additional properties or methods.

---

## Conclusion
In conclusion, **types** and **interfaces** are important concepts in TypeScript that can be used to enforce type consistency and structure in your code. Types are a more general way to describe the structure of a value, and can include basic types like strings and numbers, as well as more **complex** types like arrays and objects. 
Interfaces are a more specific and rigid way to describe the structure of an **object**, and define a set of properties and methods that an object should have. Both types and interfaces can be useful in different situations, and it's important to understand the differences between the two and when to use each one in order to effectively use TypeScript in your projects.