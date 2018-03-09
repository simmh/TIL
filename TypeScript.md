# TypeScript



## TypeScript - **Intro & Install**

## 1 TypeScript의 소개와 개발 환경 구축

### 1. Introduction

자바스크립트는 다음과 같은 특성으로 코드가 복잡해짐. 디버그와 테스트 공수가 증가 등 문제를 야기시킬 수 있다. 대규모 개발 시에는 주의하여야 한다.



< JavaScrip의 다른 C-family 언어와 구별되는 대표적인 특징 >

* Prototype-based Object Oriented Language
* Scope와 this
* 동적 타입(dynamic typed) 언어 혹은 느슨한 타입(loosely typed) 언어



TypeScript 또한 AltJS의 하나로써 **JavaScript(ES5)의 Superset(상위확장)**이다. 
C#의 창시자인 덴마크 출신 소프트웨어 엔지니어 [Anders Hejlsberg(아네르스 하일스베르)](https://en.wikipedia.org/wiki/Anders_Hejlsberg)가 개발을 주도



< TypeScript의 장점 >

* TypeScript는 정적 타입을 지원하므로 컴파일 단계에서 오류를 포착할 수 있는 다. 
* 명시적인 정적 타입 지정은 개발자의 의도를 명확히 코드에 기술할 수 있다. 
* 이는 코드의 가독성을 향상 시키고 예측을 가능하게 하며 디버깅을 쉽게 한다.



### 2. TypeScript를 사용하는 이유

* 정적 타입 - 컴파일 단계에서 오류 포착. 개발자의 의도를 명확히 코드에 기술.


* 도구의 지원 - IDE에 타입 정보를 제공함으로써 높은 수준의 IntelliSense, 코드 어시스트, 타입 체크, 리팩토링 등을 지원 받음
* 강력한 OOP 지원 - 인터페이스, 제네릭 등 OOP지원으로 크고 복잡한 프로젝트 코드 기반 쉽게 구축 (ex.제네릭: todo type?)
* ES6 / ES Next 지원
* Angular



### 3. 개발환경 구축

```java
// 1. Node.js 설치 (npm 같이 설치 됨)
// 2. 전역에 TypeScript 설치
npm install -g typescript

// 버전 확인
$ tsc -v
Version 2.6.2

```



트랜스파일링 (바벨 필요없다, 웹펙의 모듈로더 기능도 함 브라우저 불가능 그래서 웹펙쓴다)

```javascript
// 같은 디렉터리에 js 파일 생성 (.ts 확장명 생략 가능)
> tsc {{파일명}} 

// js 버전 지정 
tsc {{파일명}} -t es6

// 두개 파일 트랜스 후 실행
tsc person.ts student.ts
node student

// 와일드카드 사용 모두 트랜스 후 실행
tsc *.ts
$ node student

// 와치모드
tsc student.ts --watch
```



## 2 TypeScript - **Typing**

## 타입 선언과 정적 타이핑

### 1. 타입 선언 (Type Declaration)

```typescript
// 변수명: 타입
let foo: string = 'hello';

// 타입과 맞기 않는 값 할당시 컴파일 시점에 에러.
let bar: number = true;

// 함수선언식
// 매개변수 타입 (안할땐 초기값)필수x
// 마지막은 리턴타입. 필수x
function multiply1(x: number, y: number): number {
  return x * y;
}

// 함수표현식
const multiply2 = (x: number, y: number): number => x * y;
console.log(multiply1(true, 1)); // error TS2345
// 함수에 방어코드 없어도되서 편하다
```



### 2. 정적 타이핑 (Static Typing)

< TypeScript 의 별도 타입 >

arry, tuple, enum, any, void, never

```typescript
// boolean
let isDone: boolean = false;

// null
let n: null = null;

// undefined
let u: undefined = undefined;

// number
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;

// string
let color: string = "blue";
color = 'red';
let myName: string = `Lee`; // ES6 템플릿 문자열
let greeting: string = `Hello, my name is ${ myName }.`; // ES6 템플릿 대입문

// object
const obj: object = {};

// array
let list1: any[] = [1, 'two', true];
let list2: number[] = [1, 2, 3]; //배열 때 쓴다
let list3: Array<number> = [1, 2, 3]; // Generic array type


// tuple : 고정된 요소수 만큼의 타입을 미리 선언후 배열을 표현
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ['hello', 10]; // OK
// Initialize it incorrectly
x = [10, 'hello']; // Error

console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'

// enum : 열거형은 숫자값 집합에 이름을 지정한 것.
/* 
ex. TodoStatus {'All','Active','Completed'};
let status = TodoStatus.All; 
*/

enum Color1 {Red, Green, Blue};
let c1: Color1 = Color1.Green;

console.log(c1); // 1

enum Color2 {Red = 1, Green, Blue};
let c2: Color2 = Color2.Green;

console.log(c2); // 2

enum Color3 {Red = 1, Green = 2, Blue = 4};
let c3: Color3 = Color3.Blue;

console.log(c3); // 4

// any : 타입 추론(type inference)할 수 없거나 타입 체크가 필요없는 변수는 any 타입으로 선언한다.
let notSure: any = 4;
notSure = 'maybe a string instead';
notSure = false; // okay, definitely a boolean

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



<타입 생략시>

* 동적으로 타입이 결정(타입추론: Type Inference)
* 타입 추론으로 자료형이 결정된 이후 다른 타입의 값을 할당하면 에러



< 정적 타입의 장점 >

정적 타이팅의 장점은 **코드 가독성, 예측성, 안정성의 향상**이라고 볼 수 있는데 이는 대규모 프로젝트에 매우 적합하다.



## 3. TypeScript - **Class** 클래스

1 클래스 정의 (Class Definition)

ES6 클래스

* 기존 prototype 기반 패턴의 Syntactic sugar
* constructor 멤버 변수 선언. 
* 결국 멤버 변수 모두 퍼플릭 하다.



```typescript
// person.ts
class Person {
  // 멤버 변수를 사전 선언하여야 한다
  name: string; //(1)

  constructor(name: string) {
    // 멤버 변수에 값을 할당
    this.name = name; //(1) === name: string
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}

const person = new Foo('Lee');
person.walk(); // Lee is walking
```



2 접근 제한자 (Access modifier)

```typescript
class Foo {
  public x: string; // (1) 맴버 변수
  protected y: string;
  private z: string;

  constructor(x: string, y: string, z: string) {
    // public, protected, private 접근 제한자 모두 클래스 내부에서 참조 가능하다.
    this.x = x;
    this.y = y;
    this.z = z;
  }
}

// public만 참조 가능
const foo = new Foo('x', 'y', 'z'); 

// (1) 부분은 결국 매개변수에서 초기화 하기에 생략
class Bar extends Foo {
  constructor(x: string, y: string, z: string) {
    super(x, y, z);
```

```
note.
class 왜 기본 privite ?
공개시 사용자가 알려고 한다. 알필요 없으면 정보 은닉.

다른 언어에선 getter setter로만 참조 하는 공식.
```



```typescript
class Foo {
  // x는 생성자 내부에서만 유효한 지역 변수이다.
  constructor(x: string) { // this로 못받
    console.log(x);
  }
}

const foo = new Foo('Hello');
console.log(foo); // Foo {}
```



3 생성자 파라미터에 접근 제한자 선언



4 readonly 키워드

멤버 변수에 let,const 안쓰는 대신 상수 표현은 readonly ;

```
note.
대부분 상수는 외부에 노출 안한다.
```



5 static 키워드



6 추상 클래스 (Abstract class)

상속 되어지기 위한 클래스

```typescript
abstract class Animal { // 틀
  // 추상 메소드
  abstract makeSound(): void;
  // 일반 메소드
  move(): void {
    console.log('roaming the earth...');
  }
}

// new Animal();
// error TS2511: Cannot create an instance of the abstract class 'Animal'.

class Dog extends Animal {
  // 추상 클래스의 추상 메소드를 반드시 구현하여야 한다
  makeSound() {
    console.log('bowwow~~');
  }
}

const myDog = new Dog();
myDog.makeSound();
myDog.move();
person.walk(); // Lee is walking
```



## *12.5* TypeScript - **Interface**

## 인터페이스

### 1. Introduction

인터페이스는 

* 일반적으로 **타입 체크를 위해 사용되며 일반 변수, 함수, 클래스에 사용**할 수 있다
* 여러가지 자료형을 갖는 프로퍼티로 이루어진 새로운 자료형을 정의하는 것과 유사.
* 선언된 프로퍼티 또는 메소드의 구현을 강제하여 일관성을 유지할 수 있도록 하는 것
* ES6는 인터페이스를 지원하지 않지만 TypeScript는 인터페이스를 지원.

### 2 변수와 인터페이스

<함수에 파라미터로 인터페이스 사용>

* 인터페이스로 함수 파라미터의 타입을 선언가능
* 해당 함수에는 함수 파라미터의 타입으로 지정한 인터페이스를 준수하는 인수를 전달하여야 한다
* 함수에 객체를 전달할 때 복잡한 매개변수 체크가 필요없어서 매우 유용



### 3 함수와 인터페이스

```typescript
// 사용빈도 낮음
// 함수 인터페이스의 정의
interface SquareFunc {
  (num: number): number;
}

// 함수 인테페이스를 구현하는 함수는 인터페이스를 준수하여야 한다.
const squareFunc: SquareFunc = function (num: number) {
  return num * num;
}

console.log(squareFunc(10)); // 100
```



4 클래스와 인터페이스 

```typescript
// 인터페이스의 정의
interface ITodo {
  id: number;
  content: string;
  completed: boolean;
}

// Todo 클래스는 ITodo 인터페이스를 구현하여야 한다.
class Todo implements ITodo {
  constructor (
    public id: number,
    public content: string,
    public completed: boolean
  ) { }
}

const todo = new Todo(1, 'Typescript', false);

console.log(todo);
```



5 덕 타이핑(Duck typing)

interface 를  implements 안했어도 (중요한게 아님) 같은 메소드 (값) 구현 했다면 자동으로 같은  해당 interface 타입으로 본다.
다른 말로 구조적 타이핑 이라함.



6 선택적 프로퍼티 (Optional Property)

선택적 프로퍼티는 프로퍼티명 뒤에 `?`를 붙이며 생략하여도 에러가 발생하지 않는다.

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
```



## *12.6* TypeScript - **Generic**

## 제네릭

**제네릭은 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법이다. 한번의 선언으로 다양한 타입에 재사용이 가능하다는 장점이 있다.**

**T는 제네릭을 선언할 때 관용적으로 사용되는 식별자로 타입 파라미터(Type parameter)라 한다**

