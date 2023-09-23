# Typescript

# Module 2

- Type Alias

```ts
type CrushType = {
  name: string;
  age?: number;
  profession: string;
  address: string;
};

const crush1: CrushType = {
  name: "Moina Pakhi",
  age: 22,
  profession: "Web Developer",
  address: "Uganda",
};

type OperationType = (x: number, y: number) => number;

const calculate = (
  number1: number, // 10
  number2: number, //20
  operation: OperationType // (x, y) => x - y)  (10,20)=>10-20
) => {
  return operation(number1, number2);
};

calculate(10, 20, (x, y) => x + y);
calculate(10, 20, (x, y) => x - y);
calculate(10, 20, (x, y) => x * y);
```

- Array

```ts
const names: string[] = ["abul", "babul", "kabul"];
const numbers: number[] = [12, 2, 3, 4, 5, 6, 6, 5];

numbers[3] = 3;
```

- Function

```ts
function addTwo(a: number, b: number) {
  return a + b;
}
console.log(addTwo(12, 33));

const addThree = (a: string, b: string) => {
  return a + " " + b;
};
console.log(addThree("Mrs", " Khadija"));

const personTwo: {
  name: string;
  balance: number;
  addBalance(money: number): void;
} = {
  name: "Apple",
  balance: 22,
  addBalance(money: number) {
    console.log(`My new Balance is ${this.balance + money}`);
  },
};
```

- Null Unknown Never

```ts
const searchName = (value: string | null) => {
  if (value === null) {
    console.log("There is nothing to search");
  } else {
    console.log("Searching...");
  }
};

searchName(null);

// kmh^-1 --> ms^-1

const getMyCarSpeed = (speed: unknown) => {
  if (typeof speed === "number") {
    const convertedSpeed = (speed * 1000) / 3600;
    console.log(`My speed is ${convertedSpeed}`);
  }
  if (typeof speed === "string") {
    const [value, unit] = speed.split(" "); // ['10' ,'kmh^-1']

    const convertedSpeed = (parseFloat(value) * 1000) / 3600;
    console.log(`My speed is ${convertedSpeed}`);
  } else {
    console.log("There is wrong type");
  }
};

getMyCarSpeed(10);
getMyCarSpeed("10 kmh^-1"); // 10 kmh-1
getMyCarSpeed(true);

function throwError(message: string): never {
  throw new Error(message);
}
```

- Object

```ts
const user: {
  name: string;
  age: number;
  isMarried?: boolean;
  readonly gender: string;
} = {
  name: "Khadija",
  age: 12,
  isMarried: false,
  gender: "female",
};
```

- Question Mark

```ts
//ternary operator
const age: number = 15;
const isAdult = age >= 18 ? " Yes" : "No";

// Nullish Coalescence Operator
// Null and Undefined

const isAuthenticatedUser = "";
const userName = isAuthenticatedUser ?? "Guest";
const userName2 = isAuthenticatedUser ? isAuthenticatedUser : "Guest";

console.log({ userName }, { userName2 });

type Manush = {
  name: string;
  age: number;
  address: {
    city: "NO City";
    road: "No Road";
    home?: "";
  };
};

const manush1: Manush = {
  name: "Manush",
  age: 40,
  address: {
    city: "NO City",
    road: "No Road",
  },
};

const home = manush1?.address?.home ?? "No Home"; // default 'No Home'
console.log({ home });
```

- Rest Operator

```ts
const greetFriends = (...friends: string[]): void => {
  friends.forEach((friend) => console.log(`${friend}`));
};

greetFriends("Abul", "Kabul", "Babul", "Labul");

const myFriends = ["Abul", "Rahim", "Karim"];
const newFriends = ["Liton", "Shakib", "Miraz"];

myFriends.push(...newFriends);
console.log(myFriends);
```

- Union Intersection

```ts
type NoobDeveloper = {
  name: string;
};

// type JuniorDeveloper = {
//   name: string;
//   expertise: string;
//   experience: number;
// };

type JuniorDeveloper = NoobDeveloper & {
  expertise: string;
  experience: number;
};

// enum Level = {
//     junior="junior",
//     mid = "mid",
//     senior = "senior"
// }

type NextLevelDeveloper = JuniorDeveloper & {
  leadershipExperience: number;
  level: "junior" | "mid" | "senior";
};

const newDeveloper: NoobDeveloper | JuniorDeveloper = {
  name: "Moznu Mia",
  expertise: "Javascript",
  experience: 1,
};

const developer: NextLevelDeveloper = {
  name: "Next Bhai",
  expertise: "Typescript",
  experience: 2,
  leadershipExperience: 1,
  level: "senior",
};
```

# Module 3

- Asynchronous

```ts
interface ITodo {
  userId: number;
  id: number;
  title: string;
  completed: boolean;
}

const getTodo = async (): Promise<ITodo> => {
  const response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
  const data = await response.json();
  return data;
};

const getTodoData = async (): Promise<void> => {
  const todo = await getTodo();
  console.log(todo);
};

getTodoData();

const makePromise = (): Promise<string> => {
  return new Promise<string>((resolve, reject) => {
    const data: string = "Data is Fetched from the server";
    if (data) {
      resolve(data);
    } else {
      reject("Failed to fetch data");
    }
  });
};

const makePromiseBoolean = (): Promise<boolean> => {
  return new Promise<boolean>((resolve, reject) => {
    const data: boolean = true;
    if (data) {
      resolve(data);
    } else {
      reject("Failed to fetch data");
    }
  });
};

type DataType = {
  id: number;
  name: string;
  age: number;
  address: {
    city: string;
    state: string;
    country: string;
  };
};

const makePromiseObject = (): Promise<DataType> => {
  return new Promise<DataType>((resolve, reject) => {
    const data: DataType = {
      id: 1,
      name: "John Doe",
      age: 30,
      address: {
        city: "New York",
        state: "NY",
        country: "USA",
      },
    };
    if (data) {
      resolve(data);
    } else {
      reject("Failed to fetch data");
    }
  });
};

// const makePromiseObject = (): Promise<object> => {
//   return new Promise<object>((resolve, reject) => {
//     const data: object = {
//         id: 1,
//         name: "John Doe",
//         age: 30,
//         address: {
//             city: "New York",
//             state: "NY",
//             country: "USA"
//         }
//     };
//     if (data) {
//       resolve(data);
//     } else {
//       reject("Failed to fetch data");
//     }
//   });
// };

const getPromiseData = async (): Promise<string> => {
  const data = await makePromise();
  return data;
};

const getPromiseDataBoolean = async (): Promise<boolean> => {
  const data = await makePromiseBoolean();
  return data;
};

const getPromiseDataObject = async (): Promise<DataType> => {
  const data = await makePromiseObject();
  return data;
};

// Promise<string> Promise<boolean> Promise<object>
```

- Conditional Types

```ts
// a type is dependent on another type

type a1 = number;
type a3 = undefined;
type a4 = number;

type a2 = a1 extends string ? string : null;
//nested conditional type
type d = a1 extends null
  ? null
  : a3 extends number
  ? number
  : a4 extends null
  ? null
  : never;

type Sheikh = {
  wife1: string;
  wife2: string;
};

// type A = keyof Sheikh; // 'wife1' | 'wife2'
// 'wife3' extends 'wife1' | 'wife2
type CheckProperty<T, K> = K extends keyof Sheikh ? true : false;

type CheckWife2 = CheckProperty<Sheikh, "girlfriend">;

// check korbe ei Sheikh Type a wife3 ase kina ? true : false

//Matha Kharap Example

type Bandhubi = "Monika" | "Rachel" | "Pheobe";

type RemoveBadhubi<T, K> = T extends K ? never : T;

type CurrentBandhubi = RemoveBadhubi<Bandhubi, "Rachel">;
```

- Generic Constrains

```ts
// const newData = {...myInfo ,crush};

type MandatoryTypes = { name: string; age: number; salary: number };
interface MandatoryInterface {
  name: string;
  age: number;
  salary: number;
}

const addMeInMyCrushMind = <T extends MandatoryInterface>(myInfo: T) => {
  const crush = "kate Winslet";
  const newData = { ...myInfo, crush };
  return newData;
};

type MyInFoType = {
  name: string;
  age: number;
  salary: number;
  other1: boolean;
  other2: null;
};
const myInfo = {
  name: "Persian",
  age: 100,
  salary: 100000000,
  other1: false,
  other2: null,
};
const result5 = addMeInMyCrushMind(myInfo);
```

- Generic Function

```ts
// Arrow Function
const createArray = (param: string): string[] => {
  return [param];
};

const result1 = createArray("Bangladesh");

const result2 = createArray("United States of America");

const createArray = (param: string): string[] => {
  return [param];
};

const createArray2 = <T>(param: T): T[] => {
  return [param];
};

const result1 = createArray("Bangladesh");

const result2 = createArray2<string>("United States of America");

const result3 = createArray2<boolean>(true);

const result4 = createArray2<number>(1);

const result5 = createArray2<object>({ name: "Bangladesh" });

type Name = { name: string };
const result51 = createArray2<Name>({ name: "Bangladesh" });

// Spread Operator

const newData = { ...myInfo, crush };
const addMeInMyCrushMind = <T>(myInfo: T) => {
  const crush = "kate Winslet";
  const newData = { ...myInfo, crush };
  return newData;
};

const myInfo = {
  name: "Persian",
  age: 100,
  salary: 100000000,
};
const result6 = addMeInMyCrushMind(myInfo);
result6.crush;
```

- Generic Interface

```ts
// Generic Interface

interface CrushInterface<T, U = null> {
  name: string;
  husband: T;
  wife?: U;
}

interface PersonInterface {
  name: string;
  age: number;
}

const crush4: CrushInterface<PersonInterface, PersonInterface> = {
  name: "Kate",
  husband: {
    name: "Persian",
    age: 30,
  },
  wife: {
    name: "Winslet",
    age: 40,
  },
};

const crush1: CrushInterface<boolean, string> = {
  name: "Kate Winslet",
  husband: true,
  wife: "Chokina",
};

const crush2: CrushInterface<string> = {
  name: "Kate Winslet",
  husband: "Persian",
};

interface HusbandInterface {
  name: string;
  salary: number;
}

const crush3: CrushInterface<HusbandInterface> = {
  name: "Kate Winslet",
  husband: {
    name: "Persian",
    salary: 0.01,
  },
};

type GenericTuple<X, Y> = [X, Y];

const relation: GenericTuple<string, string> = ["Persian", "Kate Winslet"];

type RelationWithSalaryType = { name: string; salary: number };

interface RelationWithSalaryInterface {
  name: string;
  salary: number;
}

const relationWithSalary: GenericTuple<RelationWithSalaryInterface, string> = [
  {
    name: "Persian",
    salary: 1000000000,
  },
  "Kate Winslet",
];

const relationWithSalary2: GenericTuple<RelationWithSalaryType, string> = [
  {
    name: "Persian",
    salary: 1000000000,
  },
  "Kate Winslet",
];

type GenericArray<T> = Array<T>;

// const rollNumbers: GenericArray<number> = [44, 12, 4];
const rollNumbers2: GenericArray<string> = ["44", "12", "4"];
const rollNumbers3: GenericArray<boolean> = [true, false];

type NameRollType = { name: string; roll: number };

const userNameAndRollNumbers: GenericArray<NameRollType> = [
  {
    name: "Mr. X",
    roll: 1,
  },
  {
    name: "Mr. Y",
    roll: 2,
  },
];
```

- Generic keyOf Constraints

```ts
type PersonType = {
  name: string;
  age: number;
  address: string;
};

type newType = "name" | "age" | "address"; // manully korsi

type newTypeUsingKeyOf = keyof PersonType;

// const a: newType= 'age'
// const b: newTypeUsingKeyOf='hh'

// Y = 'name' |'age'

function getProperty<X, Y extends keyof X>(obj: X, key: Y) {
  obj[key];
}

const property = getProperty({ name: "Mr.X", age: 100 }, "age");

// ({name: 'Mr.X' ,age:100} , 'age')  //100
// const a={
//   name: 'Mr.X' ,age:100
// }
// a['age']
```

- Generic Types

```ts
type GenericArray<T> = Array<T>;

const rollNumbers: GenericArray<number> = [1, 2, 3, 4, 5, 6, 7, 8, 9];

const rollNumbers2: GenericArray<string> = ["1", "2", "3"];

type NameRollType = { name: string; roll: number };

const NameAndRollNumbers: GenericArray<NameRollType> = [
  {
    name: "John",
    roll: 1,
  },
  {
    name: "Jane",
    roll: 2,
  },
  {
    name: "Mary",
    roll: 3,
  },
  {
    name: "Mike",
    roll: 4,
  },
  {
    name: "Mile",
    roll: 5,
  },
];

console.log(NameAndRollNumbers);

type GenericTuple<X, Y> = [X, Y];

const relation: GenericTuple<string, string> = ["Persian", "Kate Winslet"];

type RelationWithSalaryType = { name: string; salary: number };

interface RelationWithSalaryInterface {
  name: string;
  salary: number;
}

const relationWithSalary: GenericTuple<RelationWithSalaryInterface, string> = [
  {
    name: "Persian",
    salary: 1000000000,
  },
  "Kate Winslet",
];

const relationWithSalary2: GenericTuple<RelationWithSalaryType, string> = [
  {
    name: "Persian",
    salary: 1000000000,
  },
  "Kate Winslet",
];
```

- Interface

```ts
type User = {
  name: string;
  age: number;
};

type extendedUser = User & {
  role: string;
};

interface IUser {
  name: string;
  age: number;
}

interface IExtendedUser extends IUser {
  role: string;
}

type rollNumber = number;

//Object , Function , Array

type addNumbersType = (num1: number, num2: number) => number;

interface IAddNumbers {
  (num1: number, num2: number): number;
}

type rollNumbersType = number[];
interface IRollNumbers {
  [index: number]: string;
}
const rollNumbers: IRollNumbers = ["1", "4", "5"]; //[index]

const addNumbers: addNumbersType = (num1, num2) => num1 + num2;

const user: extendedUser = {
  name: "Omanush",
  age: 2000,
  role: "Unknown",
};
const userWithTypeAlias: User = {
  name: "Type Alias",
  age: 100,
};

const userWithInterface: IUser = {
  name: "Interface",
  age: 200,
};
userWithInterface.age;
```

- Mapped Types

```ts
const arrayOfNumbers = [1, 2, 3];
const arrayOfStrings = arrayOfNumbers.map((num) => num.toString());
console.log(arrayOfStrings);

type AreaNumber = {
  height: number;
  width: number;
};

type AreaString = {
  height: string;
  width: string;
};

const rectangularArea: AreaNumber = {
  height: 10,
  width: 12,
};

type A = AreaNumber["height"]; // look up types
type B = keyof AreaNumber; // 'width' | 'height'

const obj = {
  name: "Persian",
};
obj["name"];
```

- Type Assertion

```ts
let checkbox: any;

checkbox = "Next Level Web Application";

(checkbox as string).length;
<string>checkbox.length;

function kgToGram(param: number | string): string | number | undefined {
  if (typeof param === "number") {
    return param * 1000;
  }
  if (typeof param === "string") {
    const result = parseInt(param, 10);
    return result;
  }
  return undefined;
}

kgToGram(1000) as number;
kgToGram("1000") as string;

const resultToBeNumber = kgToGram(1000) as number;
const resultToBeString = kgToGram("1000") as string;

type CustomError = {
  message: string;
};

try {
} catch (error) {
  console.log((error as CustomError).message);
}

<number>kgToGram(1000.5);
<string>kgToGram("1000.5");
```

# Module 4

# Advanced Topics

- Access Modifiers

```ts
class BankAccount {
  public readonly id: number;
  public name: string;
  protected _balance: number;

  constructor(id: number, name: string, balance: number) {
    this.id = id;
    this.name = name;
    this._balance = balance;
  }
  getBalance() {
    console.log(`My Current Balance is : ${this._balance}`);
  }
  addDeposit(amount: number) {
    this._balance = this._balance + amount;
  }
}

class StudentAccount extends BankAccount {
  test() {
    this.getBalance();
  }
}

const myAccount = new BankAccount(444, "Persian", 20);
myAccount.addDeposit(20);
myAccount.getBalance();

type Add = (a: number, b: number) => number;

const add: Add = (a, b) => {
  return a + b;
};

// const sum = add(2, 3); // 5

class Calculator {
  add(a: number, b: number): number {
    return a + b;
  }
}

const calculator = new Calculator();
const sum = calculator.add(2, 3); // 5
```

- Getter & Setter

```ts
class BankAccount {
  public readonly id: number;
  public name: string;
  private _balance: number;

  constructor(id: number, name: string, balance: number) {
    this.id = id;
    this.name = name;
    this._balance = balance;
  }

  private getTestBalance(): number {
    return this._balance;
  }

  get Test(): number {
    return this.getTestBalance();
  }
  //getter
  get balance(): number {
    return this._balance;
  }
  // getBalance(): number {
  //   return this._balance;
  // }

  //setter
  set deposit(amount: number) {
    this._balance = this.balance + amount;
  }
  // addDeposit(amount: number) {
  //   this._balance = this._balance + amount;
  // }
}

class StudentAccount extends BankAccount {
  test() {
    this.balance;
  }
}

const myAccount = new BankAccount(444, "Persian", 30);
// myAccount.addDeposit(20);
// myAccount.getBalance();
// myAccount.getBalance();
console.log(myAccount.balance);
myAccount.deposit = 30;
console.log(myAccount.balance);
```

- Inheritance

```ts
class Parent {
  name: string;
  age: number;
  address: string;
  phone: number;

  constructor(name: string, age: number, address: string, phone: number) {
    this.name = name;
    this.age = age;
    this.address = address;
    this.phone = phone;
  }

  makeSleep(hours: number) {
    return `This ${this.name} will sleep for ${hours}`;
  }
}

class Student extends Parent {
  constructor(name: string, age: number, address: string, phone: number) {
    super(name, age, address, phone);
  }
}

const student1 = new Student("John", 22, "NYC", 1332234433);
console.log(student1);

class Teacher extends Parent {
  designation: string;

  constructor(
    name: string,
    age: number,
    address: string,
    phone: number,
    designation: string
  ) {
    super(name, age, address, phone);
    this.designation = designation;
  }

  takeClasses(numberOfClass: number) {
    return `This ${this.name} will take classes ${numberOfClass}`;
  }
}

class Teacher1 extends Student {
  constructor(name: string, age: number, address: string, phone: number) {
    super(name, age, address, phone);
  }

  makeCity() {
    return `This ${this.name} is City for ${this.address}`;
  }
}

let student = new Student("张三", 18, "北京", 1888888888);
let teacher = new Teacher1("张三", 18, "北京", 1888888888);

console.log(student);
console.log(teacher);
```

- Object

```ts
class Animal {
  // public name: string;
  // public species: string;
  // public sound: string;

  // Parameter Properties
  constructor(
    public name: string,
    public species: string,
    public sound: string
  ) {
    // this.name = name;
    // this.species = species;
    // this.sound = sound;
    // console.log(this.name);
  }
  public makeSound() {
    console.log(`My name is ${this.name} says ${this.sound}`);
  }
}

const dog = new Animal("German Shepard", "Dog", "Ghew, Ghew");
const cat = new Animal("Persian", "Cat", "Mew Mew");

cat.makeSound();
dog.makeSound();
```

- Polymorphism

```ts
class Person {
  takeNap(): void {
    console.log("I am sleeping 8 hours per day");
  }
}

class Student extends Person {
  takeNap(): void {
    console.log(`I am sleeping 10 hours per day`);
  }
}

class Developer extends Person {
  takeNap(): void {
    console.log(`I am sleeping 5 hours per day`);
  }
}

function getNap(param: Person) {
  param.takeNap();
}

const person1 = new Person();
const person2 = new Student();
const person3 = new Developer();
getNap(person1);
getNap(person2);
getNap(person3);

class Shape {
  getArea(): number {
    return 0;
  }
}

// area -> pi * r * r
class Circle extends Shape {
  radius: number;
  constructor(radius: number) {
    super();
    this.radius = radius;
  }
  getArea(): number {
    return Math.PI * this.radius * this.radius;
  }
}

class Rectangle extends Shape {
  height: number;
  width: number;
  constructor(height: number, width: number) {
    super();
    this.height = height;
    this.width = width;
  }
  getArea(): number {
    return this.width * this.height;
  }
}

function getAreaOfShape(param: Shape) {
  console.log(param.getArea());
}

getAreaOfShape(new Circle(10));
getAreaOfShape(new Rectangle(10, 12));
```

- Statics

```ts
class Counter {
  static counter: number = 0;

  static increment(): number {
    return (Counter.counter = Counter.counter + 1);
  }
  static decrement(): number {
    return (Counter.counter = Counter.counter - 1);
  }
}

// const instance1 = new Counter();
// const instance2 = new Counter();
console.log(Counter.increment()); // 0-1
console.log(Counter.increment()); // 1-2
```

- Type-Guard-Narrowing

```ts
//keyof guard
type Alphanumeric = string | number;
// keyof guard
function add(param1: Alphanumeric, param2: Alphanumeric): Alphanumeric {
  if (typeof param1 == "number" && typeof param2 === "number") {
    return param1 + param2;
  } else {
    return param1.toString() + param2.toString();
  }
}

add("1", "2");
add(1, 2);

//in guard

type NormalUserType = {
  name: string;
};

type AdminUserType = {
  name: string;
  role: "admin";
};

function getUser(user: NormalUserType | AdminUserType): string {
  if ("role" in user) {
    return `I am an admin and my role is ${user.role}`;
  } else {
    return `I am a normal user`;
  }
}

const normalUser1: NormalUserType = { name: "Mr. kallu" };
const adminUser1: AdminUserType = { name: "Mr. Gallu", role: "admin" };

console.log(getUser(normalUser1));
console.log(getUser(adminUser1));

//instanceof guard

class Animal {
  name: string;
  species: string;
  constructor(name: string, species: string) {
    this.name = name;
    this.species = species;
  }

  makeSound() {
    console.log("I am making sound");
  }
}

class Dog extends Animal {
  constructor(name: string, species: string) {
    super(name, species);
  }
  makeBark() {
    console.log(" I am barking");
  }
}
class Cat extends Animal {
  constructor(name: string, species: string) {
    super(name, species);
  }
  makeMew() {
    console.log("I am Mewing");
  }
}

function isDog(animal: Animal): animal is Dog {
  return animal instanceof Dog;
}

function isCat(animal: Animal): animal is Cat {
  return animal instanceof Cat;
}

function getAnimal(animal: Animal) {
  if (isDog(animal)) {
    animal.makeBark();
  } else if (isCat(animal)) {
    animal.makeMew();
  } else {
    animal.makeSound();
  }
}

const animal1 = new Dog("German Bhai", "dog"); // instance -> Dog
const animal2 = new Cat("Persian Bhai", "cat"); // instance -> Cat

getAnimal(animal2);
```

# Assignment

```ts
// Problem 1
/**
 * Create a TypeScript program that declares a function that takes two parameters, a string and a number. The function should log the string parameter repeated the number of times specified by the number parameter. If the number parameter is not provided, it should default to 3
 */

function repeatedString(str: string, num: number = 3): void {
  for (let i = 0; i < num; i++) {
    console.log(str);
  }
}

repeatedString("Khadija");
repeatedString("Mishu", 5);

// Problem 2
/**
 * Write a function that takes in an array of objects with properties name and age, and returns only the objects where the person's age is greater than or equal to 18,
 */

function filterAdults(...peopleArray: object[]) {
  return peopleArray.filter((person: any) => person.age >= 18);
}

const people = [
  { name: "Khadija", age: 20 },
  { name: "Mishu", age: 17 },
  { name: "Mim", age: 25 },
  { name: "Didar", age: 16 },
];

const adults = filterAdults(people);
console.log(adults);

export {};

// Problem 3
/**
 * Create a TypeScript program that uses a generic function to reverse an array of strings, and takes a variable number of strings to the array using rest parameters. Provide an example of calling the function with a variable number of strings.
 */

function reverseArray<T>(...array: T[]): T[] {
  return array.reverse();
}

const fruits = ["apple", "banana", "orange"];
const reversedFruits = reverseArray(...fruits);
console.log(reversedFruits);

const numbers = [1, 2, 3, 4, 5];
const reversedNumbers = reverseArray(...numbers);
console.log(reversedNumbers);

// Problem 4
/**
 * Create a TypeScript class called Person that has private properties name and age, and a public method getDetails that returns a string with the person's name and age. Use parameter properties to define and initialize the properties in the constructor.

Create a TypeScript class called Student that extends the Person class and has an additional private property grade. Define a public method getGrade that returns the student's grade. Use the super keyword to call the constructor of the Person class and initialize the name and age properties.

 */

class Person {
  constructor(private name: string, private age: number) {}

  public getDetails(): string {
    return `Name: ${this.name}, Age: ${this.age}`;
  }
}

class Student extends Person {
  constructor(name: string, age: number, private grade: string) {
    super(name, age);
  }

  public getGrade(): string {
    return `Grade: ${this.grade}`;
  }
}

const person = new Person("Khadija", 30);
console.log(person.getDetails());

const student = new Student("Mim", 20, "A");
console.log(student.getDetails());
console.log(student.getGrade());

export {};

// Problem 5
/**
 * Create a TypeScript function that takes a parameter of type unknown and uses a type guard to check whether the parameter is of type string. If it is, log the string to the console. If it is not, log an error message.
 */

function logString(param: unknown): void {
  if (typeof param === "string") {
    console.log(param);
  } else {
    throw new Error("Parameter is not a string.");
  }
}

logString("Hello, world!");
logString(123);
```

## 1. Installation typescript, nvm & ts-node-dev

- node -v
- node version manager
- nvm -v
- nvm list
- nvm install 18.16.0
- nvm use 19.8.1
- tsc -v

- tsc => typescript convert javascript
- node index.js

- tsc --init
- tsconfig.json

- npm init -y
- package.json

- npm i -D nodemon
- package.json add nodemon

- ts-node-dev install

- tsconfig.json => rootDir:src, outDir: dist

- npm i -g typescript

- tsc init
- tsconfig.json
- "outDir": "./dist",
- "rootDir": "./src",

- package.json
- "start": "ts-node-dev --respawn --transpile-only src",

- npx ts-node-dev --respawn fileName.ts
