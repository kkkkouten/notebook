[TOC]



# TypeScript



ts是js的一个超集。在此之上增加了类型的标注。

ts不像js可以在浏览器直接运行。

ts通过TSC转义器，将ts代码转化成js代码。随后使用node来运行js代码



ts

变量声明

1. 类型推断（Type Inference）(推荐使用)

  编译器根据初始值做类型推断

  ```ts
  let str =  "str1";
  str = "str2";
  str = 123;// error
  ```

2. 类型注解（推荐）

3. 类型断言（不推荐使用）

4. 类型别名

	```ts
	let a: string | number = 10;
	type myType = string | number;
	let b: myType = 10;
	```

	





##  Syntax

###  Variable

#### Boolean

```typescript
let isDone: boolean = false;
```

#### Number

- `number`表示所有数字，包括整数和浮点数。


```typescript
let decimal: number = 6.1;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

#### String

```typescript
let color: string = "blue";
let fullName: string = `John Doe`;
```

#### Array

-  使用泛型数组类型 `Array<elementType>` 或简化的 `elementType[]` 来定义数组。
- 支持二维数组，两个[[],[]]
```typescript
let mixList = [1, 2, 3, 'abc', true, null, undefined]; // 不建议使用
let list: number[] = [1, 2, 3];
let fruits: Array<string> = ["apple", "banana", "cherry"];
let twoDiomensionArray: number[][] = [
    [1, 2, 3],
    [4, 5, 6]
];
```

#### Tuple

- 元组是一个固定长度的数组，各元素可以有不同的类型。
    ```typescript
    let tuple: [string, number] = ["apple", 5];
    ```

- 元组也可以是一个不固定长度数组
	```typescript
	let flexibleLengthTuple: [number, string, number?] = [1, "abc"];
	```

#### Enum

枚举用于命名一组有限的常量值。 默认从上到下给每个枚举值赋值0，1，2

```typescript
enum Color {
    Red,
    Green,
    Blue
};
let colorChoice1: Color = Color.Green;
let colorChoice2: Color = Color[0];
```

#### Null & Undefined

null 和 undefined 分别表示值为 null 和 undefined。

```typescript
let valueNull: null = null;
let valueUndefined: undefined = undefined;
```

#### Any

any 类型可以表示任何类型的值。它用于那些不清楚或动态类型的情况。

```typescript
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false;
```

#### Void

```typescript
function sayHello(): void {
    console.log("Hello!");
}
```

#### Never

never 表示永不会返回结果的函数或抛出异常的函数。

```typescript
function throwError(message: string): never {
    throw new Error(message);
}
```

这些是 TypeScript 中的一些基础类型。通过组合和使用这些类型，可以更精确地定义变量和函数的类型，从而提高代码的可维护性和安全性。



### Function

TypeScript 中的函数与 JavaScript 中的函数非常相似，但在 TypeScript 中，可以添加类型注解来声明函数的参数类型和返回值类型，以提高代码的可读性和类型安全性。

以下是 TypeScript 中常见的函数声明方式：

#### 函数声明

代码定义了一个名为 add 的函数，它接受两个参数 x 和 y，这两个参数的类型都是 number，并且函数返回值的类型也是 number。

```typescript
  function add(x: number, y: number): number {
      return x + y;
  }
```

#### 函数表达式

这是使用函数表达式的方式，函数被赋值给了一个变量 subtract，并且添加了参数类型和返回值类型的类型注解。

```typescript
  const subtract = function (x: number, y: number): number {
      return x - y;
  };
```

#### 箭头函数

箭头函数是一种更简洁的函数声明方式，它具有隐式的返回值类型，但您仍然可以为参数添加类型注解。

```typescript
  const multiply = (x: number, y: number): number => x * y;
```

#### 可选参数和默认参数

在上面的示例中，greet 函数的第二个参数 greeting 是可选的，而 exponent 函数的 power 参数具有默认值。

```typescript
  function greet(name: string, greeting?: string): string {
      if (greeting) {
          return `${greeting}, ${name}!`;
      } else {
          return `Hello, ${name}!`;
      }
  }

  function exponent(base: number, power: number = 2): number {
      return Math.pow(base, power);
  }
```

#### 剩余参数

`...numbers` 是剩余参数语法，它允许函数接受任意数量的参数并将它们作为数组处理。

```typescript
function sum(...numbers: number[]): number {
    return numbers.reduce((acc, val) => acc + val, 0);
}
```

#### 函数重载

函数重载允许您根据不同的参数数量或类型来定义多个函数签名，以便 TypeScript 可以根据上下文选择正确的函数。

```typescript
  function greet(name: string): string;
  function greet(name: string, greeting: string): string;
  function greet(name: string, greeting?: string): string {
      if (greeting) {
          return `${greeting}, ${name}!`;
      } else {
          return `Hello, ${name}!`;
      }
  }
```

这些是 TypeScript 中声明和使用函数的一些常见方式。函数是 TypeScript 中非常重要的一部分，因为它们使您能够编写可维护、类型安全的代码。//



### Interface

在 TypeScript 中，接口（Interfaces）用于定义对象的结构和类型。接口可以描述对象的属性、方法以及可选成员，从而帮助开发者在编写代码时更好地理解和约束数据结构。以下是 TypeScript 中使用接口的基本方式：

#### 对象属性接口

定义了一个名为 Person 的接口，它规定了对象必须包含 firstName 和 lastName 两个属性，并且这两个属性的类型必须为字符串。

```typescript
  interface Person {
      firstName: string;
      lastName: string;
  }

  const person: Person = {
      firstName: "John",
      lastName: "Doe",
  };
```

#### 可选属性

year 是一个可选属性，不是必须的。

```typescript
interface Car {
    make: string;
    model: string;
    year?: number; // 可选属性
}

const myCar: Car = {
    make: "Toyota",
    model: "Camry",
};
```

#### 只读属性

使用 readonly 关键字可以定义只读属性，一旦赋值就不能再修改。

```typescript
  interface Point {
      readonly x: number;
      readonly y: number;
  }

  const point: Point = { x: 10, y: 20 };
  point.x = 5; // 错误，只读属性不可修改
```

#### 函数接口

定义了一个函数接口 Calculator，它描述了一个接受两个参数并返回一个数字的函数。

```typescript
  interface Calculator {
      (x: number, y: number): number;
  }

  const add: Calculator = (x, y) => x + y;
```

#### 类接口

定义了一个 Shape 接口，它规定了实现它的类必须包含 getArea 方法。

```typescript
  interface Shape {
      getArea(): number;
  }

  class Circle implements Shape {
      constructor(private radius: number) {}

      getArea() {
          return Math.PI * this.radius ** 2;
      }
  }
```

#### 继承接口

使用 extends 关键字可以创建一个继承其他接口的新接口。

```typescript
  interface Animal {
      name: string;
  }

  interface Bird extends Animal {
      fly: boolean;
  }

  const eagle: Bird = {
      name: "Bald Eagle",
      fly: true,
  };
```

#### 混合类型接口

创建了一个混合类型接口 Counter，它既可以作为函数调用，又可以调用其方法。

```typescript
interface Counter {
    (): number;
    increment(): void;
}

function createCounter(): Counter {
    let count = 0;

    const counter = () => count++;
    counter.increment = () => count++;

    return counter;
}

const myCounter = createCounter();
myCounter(); // 调用函数
myCounter.increment(); // 调用方法
```



这些是 TypeScript 中使用接口的一些基本方式。接口在类型定义和约束方面非常有用，可以帮助您编写更安全和可读的代码。





### Class

TypeScript 中的类（class）是一种用于创建对象的模板，它具有属性和方法，可以实现面向对象编程（OOP）的概念，如封装、继承和多态。类允许您创建具有相似特征和行为的多个对象，提高了代码的可重用性和可维护性。以下是 TypeScript 中使用类的基本概念和语法：

#### 类的定义

```typescript
class MyClass { 
    // 构造函数 
    constructor(public property1: string, private property2: number) {   
    } 
    // 方法 
    public method1() { 
        console.log("Method 1 called."); 
    } 
    private method2() { 
        console.log("Method 2 called."); 
    } 
}
```

上述代码中，定义了一个名为 `MyClass` 的类，它包含了两个属性（一个公共属性 `property1` 和一个私有属性 `property2`）以及两个方法（一个公共方法 `method1` 和一个私有方法 `method2`）。构造函数用于初始化对象的属性。

#### 类的实例化

```typescript
const instance1 = new MyClass("Value1", 42); 
const instance2 = new MyClass("Value2", 100);
```

使用 `new` 关键字可以实例化一个类，创建类的对象。每个对象都具有自己的属性值，但共享相同的方法。

#### 访问属性和方法

```typescript
console.log(instance1.property1); // 访问公共属性 
instance1.method1(); // 调用公共方法 

// 不能访问私有属性或方法 
console.log(instance1.property2); // 错误 // 
instance1.method2(); // 错误
```

公共属性和方法可以从对象实例中访问，而私有属性和方法只能在类的内部使用。

#### 类的继承

```typescript
class MySubClass extends MyClass { 
    constructor(property1: string, property2: number, public property3: boolean) { 
        super(property1, property2); // 调用父类的构造函数 
    } 
    // 重写父类的方法 
    public method1() { 
        console.log("Subclass Method 1 called."); 
    } 
    // 新的方法 
    public method3() { 
        console.log("Subclass Method 3 called."); 
    } 
}
```

子类可以继承父类的属性和方法，并且可以添加新的属性和方法。使用 `super` 关键字可以在子类的构造函数中调用父类的构造函数。

#### 多态性

```typescript
function process(obj: MyClass) { 
    obj.method1(); // 调用方法1 
} 

const obj1 = newMyClass("Value1", 42); 
const obj2 = new MySubClass("Value2", 100, true); 

process(obj1); // 调用父类的方法1 
process(obj2); // 调用子类的方法1
```

多态性允许编写通用的代码，可以处理不同子类的对象，并在运行时根据对象的实际类型来调用正确的方法。

这些是 TypeScript 中类的基本概念和语法。类是面向对象编程的核心概念之一，用于创建具有结构化和行为的对象，使代码更加模块化和可维护。



### Generic

TypeScript 中的泛型（Generics）是一种强大的工具，它允许您编写可重用和类型安全的代码，特别是在处理不同类型的数据时非常有用。泛型允许您将类型参数化，以便在函数、类和接口中使用不特定的数据类型。以下是 TypeScript 中使用泛型的一些示例和基本概念：

#### 泛型函数

identity 函数使用了泛型类型 T，它接受一个参数 arg 和一个类型参数 T，并返回与输入相同类型的值。可以显式指定类型参数，或者让 TypeScript 自动推断类型参数。

```typescript
function identity<T>(arg: T): T {
    return arg;
}

let result = identity<number>(42); // 显式指定类型参数
let strResult = identity("Hello, TypeScript!"); // 类型参数会自动推断为 string
```



#### 泛型类

在上面的示例中，Box 类使用了泛型类型 T，它可以用来包装不同类型的值。通过指定类型参数，可以创建具有特定类型的 Box 实例。

```typescript
class Box<T> {
    private value: T;

    constructor(value: T) {
        this.value = value;
    }
    
    getValue(): T {
        return this.value;
    }

}

const numberBox = new Box<number>(42);
const stringBox = new Box("Hello, TypeScript!");
```



#### 泛型接口

在上面的示例中，List 接口使用了泛型类型 T，它描述了一个通用的列表类型，可以用于不同类型的数据。

```typescript
interface List<T> {
    length: number;
    getItem(index: number): T;
}

const stringList: List<string> = {
    length: 3,
    getItem(index: number) {
        return "Item " + index;
    },
};

const numberList: List<number> = {
    length: 3,
    getItem(index: number) {
        return index * 2;
    },
};
```



#### 泛型约束

泛型约束允许您限制泛型类型的范围，确保泛型参数满足某些条件。在上述示例中，T 必须扩展具有 length 属性的类型，否则将出现类型错误。

```typescript
function loggingIdentity<T extends { length: number }>(arg: T): T {
    console.log(arg.length);
    return arg;
}

loggingIdentity([1, 2, 3]); // 合法，数组具有 length 属性
loggingIdentity("Hello");   // 合法，字符串具有 length 属性
loggingIdentity(42);        // 错误，数字没有 length 属性
```


