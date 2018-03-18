# TypeScript 



## **1 Typing** 

타입 선언과 정적 타이핑



1 타입 선언 (Type Declaration)

```typescript
let foo: string = 'hello';
```



```typescript
// 함수선언식
function multiply1(x: number, y: number): number {
  return x * y;
}

// 함수표현식
const multiply2 = (x: number, y: number): number => x * y;
```



TyperScript type

| Type      | JS   | TS   | Description                                                  |
| --------- | ---- | ---- | ------------------------------------------------------------ |
| boolean   | ◯    |      | true와 false                                                 |
| null      | ◯    |      | primitives 또는 object형 변수에 값이 없다는 것을 명시        |
| undefined | ◯    |      | 값을 할당하지 않은 변수의 초기값                             |
| number    | ◯    |      | 숫자(정수와 실수, Infinity, NaN)                             |
| string    | ◯    |      | 문자열                                                       |
| symbol    | ◯    |      | 고유하고 수정 불가능한 데이터 타입이며 주로 객체 프로퍼티들의 식별자로 사용(ES6에서 추가) |
| object    | ◯    |      | 객체형, 참조형                                               |
| array     |      | ◯    | 배열                                                         |
| tuple     |      | ◯    | 고정된 요소수 만큼의 자료형을 미리 선언후 배열을 표현        |
| enum      |      | ◯    | 열거형. 숫자값 집합에 이름을 지정한 것이다.                  |
| any       |      | ◯    | 타입 추론(type inference)할 수 없거나 타입 체크가 필요없는 변수는 any 타입으로 선언한다. |
| void      |      | ◯    | 일반적으로 함수에서 반환값이 없을 경우 사용한다.             |
| never     |      | ◯    | 결코 발생하지 않는 값                                        |

타입선연 예제

```typescript
// object
const obj: object = {};

// array
let list1: any[] = [1, 'two', true];
let list2: number[] = [1, 2, 3];
let list3: Array<number> = [1, 2, 3]; // Generic array type

// enum : 열거형은 숫자값 집합에 이름을 지정한 것.
enum Color1 {Red, Green, Blue};
let c1: Color1 = Color1.Green;
console.log(c1); // 1

enum Color2 {Red = 1, Green, Blue};
let c2: Color2 = Color2.Green;

console.log(c2); // 2

enum Color3 {Red = 1, Green = 2, Blue = 4};
let c3: Color3 = Color3.Blue;

console.log(c3); // 4

// void : 일반적으로 함수에서 반환값이 없을 경우 사용한다.
function warnUser(): void {
  console.log("This is my warning message");
}

// never : 결코 발생하지 않는 값
function infiniteLoop(): never {
  while (true) {}
}

function error(message: string): never {
  throw new Error(message);
}
```



## **2 Class** 

### 클래스 정의 (Class Definition)

**Typescript 클래스는 클래스 바디에 멤버 변수를 사전 선언하여야 한다.**

```typescript
// person.ts
class Person {
  // 멤버 변수를 사전 선언하여야 한다
  name: string;

  constructor(name: string) {
    // 멤버 변수에 값을 할당
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}

const person = new Foo('Lee');
person.walk(); // Lee is walking
```



#### 접근 제한자의 프로퍼티에 대한 접근 가능성

| 접근 가능성     | public | protected | private |
| --------------- | ------ | --------- | ------- |
| 클래스 내부     | ◯      | ◯         | ◯       |
| 자식 클래스     | ◯      | ◯         | ✕       |
| 클래스 인스턴스 | ◯      | ✕         | ✕       |

예제

```typescript
class Foo {
  public x: string;
  protected y: string;
  private z: string;

  constructor(x: string, y: string, z: string) {
    // public, protected, private 접근 제한자 모두 클래스 내부에서 참조 가능하다.
    this.x = x;
    this.y = y;
    this.z = z;
  }
}

// public  foo.x 접근 OK 
// foo.y. foo.z 접근 못함 erro
const foo = new Foo('x', 'y', 'z'); 

// 상속
class Bar extends Foo {
  constructor(x: string, y: string, z: string) {
    super(x, y, z);        
    console.log(this.x);// public. 자식 클래스에서 참조 OK   
    console.log(this.y);// protected. 자식 클래스에서 참조 OK     
    console.log(this.z);// private. 자식 클래스에서 참조 error X
  }
}
```



#### 생성자 파라미터에 접근 제한자 선언

constructor(x: string) 접근제한자 무생성시 내부에서만 참조 가능

```typescript
class Foo {
  // x는 생성자 내부에서만 유효한 지역 변수이다.
  constructor(x: string) {
    console.log(x);
  }
}

const foo = new Foo('Hello');
console.log(foo); // Foo {}
```



**접근 제한자가 사용된 생성자 파라미터는 암묵적으로 멤버 변수로 선언.**
**생성자 내부에서 별도의 초기화가 없어도 암묵적으로 초기화가 수행된다.**

```typescript
class Foo {
  // public 선언. x는 클래스 외부에서도 참조가 가능
  constructor(public x: string) { }
}

const foo = new Foo('Hello');
console.log(foo);   // Foo { x: 'Hello' }
console.log(foo.x); // Hello

class Bar {
// private 선언. x는 클래스 내부에서만 참조 가능. 
// 그럼 자동으로 암묵적 초기화 될텐데 제한자 왜 선언?
  constructor(private x: string) { }
}

const bar = new Bar('Hello');

console.log(bar); // Bar { x: 'Hello' }

// private이 선언된 bar.x는 클래스 내부에서만 참조 가능하다
console.log(bar.x); // Property 'x' is private and only accessible within class 'Bar'.
```



#### * readonly 키워드

#### * static 키워드

#### * 추상 클래스 (Abstract class) 



## 3 **Interface**

인터페이스

* 일반적으로 **타입 체크를 위해 사용되며 일반 변수, 함수, 클래스에 사용**할 수 있다.
* 여러가지 자료형을 갖는 프로퍼티로 이루어진 새로운 자료형을 정의하는 것과 유사
* 인터페이스에 선언된 프로퍼티 또는 메소드의 구현을 강제하여 일관성을 유지할 수 있도록 하는 것
* 인터페이스는 멤버변수와 메소드를 가질 수 있다는 점에서 클래스와 유사하나 직접 인스턴스를 생성할 수는 없다



### 변수와 인터페이스

인터페이스는 일반 변수의 타입으로 사용할 수 있다.

```typescript
// 인터페이스의 정의
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

// 변수 todos의 타입으로 Todo 인터페이스를 선언하였다.
let todos: Todo[];

// 변수 todos는 Todo 인터페이스를 준수하여야 한다.
todos = [
  { id: 1, content: 'typescript', completed: false }
];
```

함수 파라미터의 타입을 선언할 수 있다.

```typescript
// 파라미터 todo의 타입으로 Todo 인터페이스를 선언하였다.
function addTodo(todo: Todo) {
  console.log(todo.content);
}

// 파라미터 todo는 Todo 인터페이스를 준수하여야 한다.
const newTodo: Todo = { id: 1, content: 'typescript', completed: false };
addTodo(newTodo);
```



### 함수와 인터페이스

인터페이스는 함수의 타입으로 사용할 수 있다. 
함수의 인터페이스에는 타입이 선언된 파라미터 리스트와 리턴 타입을 정의한다. 

```typescript
// 함수 인터페이스의 정의
interface SquareFunc {
  (num: number): number;
}

// 함수 인테페이스를 구현하는 함수는 인터페이스를 준수하여야 한다.
const squareFunc: SquareFunc = function (num: number) {
  return num * num;
}

console.log(squareFunc(10)); // 10
```



### 클래스와 인터페이스

클래스 선언문의 implements 뒤에 인터페이스를 선언하면 메소드도 포함 인터페이스를 구현하는 클래스는 인터페이스에서 정의한 멤버변수와 메소드를 반드시 구현하여야 한다

```typescript
// 인터페이스의 정의
interface IPerson {
  name: string;
  sayHello(): void;
}

// 인터페이스를 구현하는 클래스는 인터페이스에서 정의한 멤버변수와 메소드를 반드시 구현하여야 한다.
class Person implements IPerson {
  // 인터페이스에서 정의한 멤버변수의 구현
  constructor(public name: string) {}

  // 인터페이스에서 정의한 메소드의 구현
  sayHello() {
    console.log(`Hello ${this.name}`);
  }
}

function greeter(person: IPerson): void {
  person.sayHello();
}

const me = new Person('Lee');
greeter(me); // Hello Lee
```

.

### 덕 타이핑 (Duck typing)

- [5. 덕 타이핑 (Duck typing)](http://poiemaweb.com/typescript-interface#5-%EB%8D%95-%ED%83%80%EC%9D%B4%ED%95%91-duck-typing)

  ​

### 선택적 프로퍼티 (Optional Property)

인터페이스의 프로퍼티가 선택적으로 필요한 경우.  선택적 프로퍼티 `?`를 붙이면 erro 발생 없음.

```typescript
interface IUserInfo {
  username: string;
  password: string;
  age?    : number;
  address?: string;
}

const userInfo: IUserInfo = {
  username: 'ungmo2@gmail.com',
  password: '123456'
}

console.log(userInfo);
```





## **4 Generic**

제네릭

* **제네릭은 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법이다. 한번의 선언으로 다양한 타입에 재사용이 가능하다는 장점이 있다.**
* **T는 제네릭을 선언할 때 관용적으로 사용되는 식별자로 타입 파라미터(Type parameter)라 한다.**   T는 Type의 약자로 반드시 T를 사용하여야 하는 것은 아니다.
* ex) 문자열에 .toFixed()를 쓰면 runtime error. 타입 명시하면 error 검출에 편리.



인수에 의해 타입매개변수가 결정된다

```typescript
class Queue<T> {
  protected data = [];
  push(item: T) {
    this.data.push(item);
  }
  pop(): T {
    return this.data.shift();
  }
}
// number 전용 Queue
const numberQueue = new Queue<number>();

numberQueue.push(0); // 매게변수 0 일때, number type으로 fix
// numberQueue.push('1'); // 의도하지 않은 실수를 사전 검출 가능
numberQueue.push(+'1');   // 실수를 사전 인지하고 수정할 수 있다

// string 전용 
const stringQueue = new Queue<string>(); 
// 커스텀 객체 전용 Queue
const myQueue = new Queue<{name: string, age: number}>();
```



함수에도 제네릭을 사용. 
제네릭을 사용하면 하나의 타입만이 아닌 다양한 타입의 매개변수와 리턴값을 사용할 수 있다.

```typescript
function reverse<T>(items: T[]): T[] {
  return items.reverse();
}

const arg = [{name: 'Lee'}, {name: 'Kim'}, {name: 'Park'}];

// 인수에 의해 타입매개변수가 결정된다
const reversed = reverse(arg); // reversed: {name: string}[]
console.log(reversed);

reversed.push({name: 100}); // Error
console.log(reversed);
```

