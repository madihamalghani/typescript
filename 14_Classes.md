# Classes:

TypeScript adds types and visibility modifiers to JavaScript classes.

## Members: Types

The members of a class (properties & methods) are typed using type annotations, similar to variables.

```jsx
class Person {
  name: string;
}

const person = new Person();
person.name = "Jane";
```

## Members: Visibility

Class members can also be given special modifiers that affect visibility.

<aside>

There are three main visibility modifiers in TypeScript.

- `public` - (default) allows access to the class member from anywhere
- `private` - only allows access to the class member from within the class
- `protected` - allows access to the class member from itself and any classes that inherit it, which is covered in the inheritance section below
</aside>

Private is accessible only within class:

```jsx
class Person {
  private name: string;

  public constructor(name: string) {
    this.name = name;
  }

  public getName(): string {
    return this.name;
  }
}

const person = new Person("Jane");
console.log(person.getName()); // person.name isn't accessible from outside the class since it's private
```

## **Parameter Properties:**

TypeScript provides a convenient way to define class members in the constructor, by adding a visibility modifier to the parameter.

```jsx
class Person {
  // name is a private member variable
  public constructor(private name: string) {}

  public getName(): string {
    return this.name;
  }
}

const person = new Person("Jane");
console.log(person.getName());
```

- `name` is **not limited to just the constructor**.
- You can use it **anywhere inside the class** (constructor + methods).
- You **cannot** use it directly **outside** the class because it’s `private`.

## Readonly

Similar to arrays, the `readonly` keyword can prevent class members from being changed.

```jsx
class Person {
  private readonly name: string;

  public constructor(name: string) {
    // name cannot be changed after this initial definition, which has to be either at its declaration or in the constructor.
    this.name = name;
  }

  public getName(): string {
    return this.name;
  }
}

const person = new Person("Jane");
console.log(person.getName());
```

- Here name is readonly so can not be changed.

## **Inheritance: Implements:**

Interfaces can be used to define the type a class must follow through the `implements` keyword.

```jsx
interface Shape {
  getArea: () => number;
}

class Rectangle implements Shape {
  public constructor(protected readonly width: number, protected readonly height: number) {}

  public getArea(): number {
    return this.width * this.height;
  }
}
```

- Interface showing ⇒structure
- Implementing interface on class

A class can implement multiple interfaces by listing each one after `implements`, separated by a comma like so: `class Rectangle implements Shape, Colored` 

```jsx
  interface Shape1 {
    getArea: () => number;
  }
  interface Colored {
    getColor: () => string;
  }
  class Rectangle implements Shape1, Colored {
    public constructor(protected readonly width: number, protected readonly height: number) {}
  
    public getArea(): number {
      return this.width * this.height;
    }
    public getColor(): string {
      return "red";
    }
  }
  const rectangle = new Rectangle(5, 10);
  console.log(rectangle.getColor(), rectangle.getArea());
```

## **Inheritance: Extends:**

Classes can extend each other through the `extends` keyword.

A class can only extend one other class.

```jsx
interface Shape2 {
    getArea: () => number;
  }
  
  class Rectangle2 implements Shape2 {
    public constructor(protected readonly width: number, protected readonly height: number) {}
  
    public getArea(): number {
      return this.width * this.height;
    }
  }
  
  class Square2 extends Rectangle2 {
    public constructor(width: number) {
      super(width, width);
    }
  
    // getArea gets inherited from Rectangle
  }
  console.log(new Square2(5).getArea(), new Rectangle2(5, 10).getArea()); //25 50
```

1. **`Shape2` interface**
    - Requires any class that implements it to have a `getArea` method returning a number.
2. **`Rectangle2`**
    - Implements `Shape2`.
    - Has two properties: `width` and `height`.
    - `getArea()` = `width * height`.
3. **`Square2`**
    - Extends `Rectangle2`.
    - A square has equal `width` and `height`, so the constructor calls:
        
        ```tsx
        super(width, width);
        
        ```
        
        which sets both width and height to the same number.
        
    - Inherits `getArea()` directly from `Rectangle2` (no need to write it again).

---

## **Override:**

When a class extends another class, it can replace the members of the parent class with the same name.

Newer versions of TypeScript allow explicitly marking this with the `override` keyword.

```jsx
interface Shape {
  getArea: () => number;
}

class Rectangle implements Shape {
  // using protected for these members allows access from classes that extend from this class, such as Square
  public constructor(protected readonly width: number, protected readonly height: number) {}

  public getArea(): number {
    return this.width * this.height;
  }

  public toString(): string {
    return `Rectangle[width=${this.width}, height=${this.height}]`;
  }
}

class Square extends Rectangle {
  public constructor(width: number) {
    super(width, width);
  }

  // this toString replaces the toString from Rectangle
  public override toString(): string {
    return `Square[width=${this.width}]`; 
  }
}
```

Note:

<aside>

By default the `override` keyword is optional when overriding a method, and only helps to prevent accidentally overriding a method that does not exist.

Use the setting `noImplicitOverride` to force it to be used when overriding.

</aside>

## **Abstract Classes:**

Classes can be written in a way that allows them to be used as a base class for other classes without having to implement all the members.

This is done by using the `abstract` keyword.

Members that are left unimplemented also use the `abstract` keyword.

```jsx
abstract class Polygon {
  public abstract getArea(): number;

  public toString(): string {
    return `Polygon[area=${this.getArea()}]`;
  }
}

class Rectangle extends Polygon {
  public constructor(protected readonly width: number, protected readonly height: number) {
    super();
  }

  public getArea(): number {
    return this.width * this.height;
  }
}
```

- **`abstract class Polygon`**
    - Can’t be used directly (you cannot do `new Polygon()`).
    - Has an **abstract method** `getArea()` → every child must implement this.
    - Has a normal method `toString()` that depends on `getArea()`.
- **`class Rectangle extends Polygon`**
    - Inherits from `Polygon`.
    - Must provide its own `getArea()` implementation.
    - `getArea()` = `width * height`.

<aside>

Abstract classes cannot be directly instantiated, as they do not have all their members implemented.

</aside>
