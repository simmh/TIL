# Javascript **Prototype**

## 프로토타입과 객체지향





## 1. 프로토타입 객체

다른 클래스기반 객체지향 프로그래밍 언어와 달리 자바스크립트는 포로토타입 기반 객체지향 프로그래밍 언어이다.

클래스 기반 객체지향 프로그래밍 언어는 객체 생성전에 클래스 정의, 객체(인스턴트) 생성.
프로토타입 기반 객체지향 프로그래밍 언어는 클래스없이 객체 생성 가능.



* 자바스크립트의 모든 객체는 자신의 부모역할 담당하는 객체와 연결되어있다.
* 이는 객체 지향의 상속 개념처럼 부모 객체의 포로퍼티, 메소드 상속 받아 사용 가능해진다.
* 이러한 부모 객체를 Prototype(프로토타입) 객체, 줄여서 Prototype(프로토타입)이라 한다.



## 2. [[Prototype]] 프로퍼티 vs prototype 프로퍼티

??? 다시정리

**[[Prototype]]프로퍼티**

* 자신의 프로토타입 객체를 가리키는 숨겨진 프로퍼티
* `__proto__` 프로퍼티로 구현되어 있다. 
* 즉 `__proto__` 과[[Prototype]] 같은 개념



* 함수를 포함한 모든 객체가 가지고 있는 프로퍼티
* **객체의 입장에서 자신의 부모 역할하는 프로토타입 객체 가리킨다.**
* **함수 객체의 경우 Function.prototype를 가리킨다.** 
  (생성자 함수로 생성된 객체의 포로토타입 체인 참조)

```javascript
console.log(Person.__proto__ === Function.prototype);
```



**prototype 프로퍼티(함수 객체의)**

* 함수도 객체라 [[prototype]] 프로퍼티 갖는다.
* 함수 객체는 일반 객체와 달리 prototype 프로퍼티도 소유.
* prototype 프로퍼티,  [[Prototype]] 프로퍼티 모두 프로토타입 객체 가리키지만 관점의 차이 있다.



* 함수 객체만 가지고 있는 프로퍼티
* **함수 객체가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모역할 하는객체(프로토타입객체)를 가리킴.**

```javascript
console.log(Person.prototype === foo.__proto__);
```



## 3. constructor 프로퍼티

프로토타입 객체는 constructor 프로퍼티를 갖는다.
constructor 프로퍼티는 객체 입장에서 자신을 생성한 객체를 가리킨다.

```javascript
function Person(name) {
  this.name = name;
}

var man = new Person('Lee');

// Person()은 생성자 함수. 
// 생성자 함수에 의해 생성된(.prototype.)
// constructor가 객체 입장에서 자신을 생성한 객체 Pserson 가리킴.
console.log(Person.prototype.constructor === Person);

// man 객체를 생성한 객체는 Person() 생성자 함수이다.
console.log(man.constructor === Person);

// Person() 생성자 함수를 생성한 객체는 Function() 생성자 함수이다.
console.log(Person.constructor === Function);
```





## 4. Prototype chain

**Prototype chain 이란?**

* 특정 객체 접근시 해당 객체에 프로퍼티나 메소드가 없다면,
* [[Prototype]] 프로퍼티가 가리키는 링크 따라 올라감.


* 부모 역할하는 프로토타입 객체의 프로퍼티나 메소드르 차례대로 검색.

```javascript
//student 객체는 hasOwnProperty 메소드 없고 호출시 에러 발생해야하나,
//student 객체의 [[Prototype]] 프로퍼티가 가리키는 링크 따라간다.
//student 객체의 부모역할 프로토타입 객체(Object.prototype)의 메소드의 메소드 hasOwnProperty를 호출

var student = {
  name: 'Lee',
  score: 90
}
console.dir(student);
// Object.prototype.hasOwnProperty()
console.log(student.hasOwnProperty('name')); // true

console.log(student.__proto__ === Object.prototype); // true
console.log(Object.prototype.hasOwnProperty('hasOwnProperty')); // true
```

함수는??



### 4.1 객 리터럴 방식으로 생성된 객체의 프로토타입 체인

객체 생성 방법은 3가지가 있다.

* 객체 리터럴
* 생성자 함수
* Object() 생성자 함수



자바스크립트 엔진이 객체 리터럴로 객체 생성 코드 만날시,
내장함수인 `Object() 생성자 함수`로 객체 생성한다. 
이를 단순화 한것 == 객체 리터럴 방식.

`Object() 생성자 함수`역시 함수다. 
따라서 함수 객체인 `Object() 생성자 함수`는 prototype프로퍼티가 있다.



??설명 다시 정리할 부분

**prototype 프로퍼티는**

- 함수 객체가 생성자로 사용될 때


- 이 함수를 통해 생성된 객체의 부모 역할을 하는 객체를 가리킨다.



**[[Prototype]] 프로퍼티는** 

- 객체의 입장에서 


- 자신의 부모 역할을 하는 프로토타입 객체을 가리킨다.


```javascript
//object 생성자 함수
var person = {
  name: 'Lee',
  gender: 'male',
  sayHello: function(){
    console.log('Hi! my name is ' + this.name);
  }
};

console.dir(person);
// 만들어진 person object의 [[prototype]] 
console.log(person.__proto__ === Object.prototype);   // ① true
console.log(Object.prototype.constructor === Object); // ② true

//object()생성자 함수가 가진 함수 prototype 프로퍼티
console.log(Object.__proto__ === Function.prototype); // ③ true
console.log(Function.prototype.__proto__ === Object.prototype); // ④ true
```



**<객체 리터럴 방식으로 생성된 객체의 프로토타입 체인** >

![Object literal Prototype chaining](http://poiemaweb.com/img/object_literal_prototype_chaining.png)



> 결론적으로 객체 리터럴을 사용하여 객체를 생성한 경우, 그 객체의 프로토타입 객체는 Object.prototype이다.





### 4.2 생성자 함수로 생성된 객체의 프로토타입 체인

생성자 함수로 객체를 생성하기 위해서는 우선 생성자 함수를 정의하여야 한다.

함수를 정의하는 방식 3가지

* 함수선언식(Function declaration)
* 함수표현식(Functin expression)
* Function() 생성자 함수



```javascript
// 함수표현식 함수정의 (함수 리터럴 방식)
var square = function(number) {
  return number * number;
};

//함수선언식 (기명함수)경우 자바스크립트 엔진이 내부적으로 기명 함수표현식으로 변환한다.
var square = function square(number) {
  return number * number;
};
```



결국 `함수선언식`, `함수 표현식` 모두 `함수 리터럴` 방식 사용.
`함수 리터럴` 방식 == `Function() 생성자 함수`로 함수 생성 단순화 한 것.



> 3가지 함수 정의 방식은 결국 Function() 생성자 함수 통해 함수 객체 생성.
> 즉, 모든 함수 객체의 prototype 객체는 Function.prototype이다.
>
> *생성자 함수도 함수 객체이므로, 
> 생성자 함수의 prototype 객체는 Function.prototype이다.



------

**<객체의 관점에서 prototype 객체>**

| 객체 생성 방식       | 엔진의 객체 생성     | 인스턴스의 prototype 객체  |
| -------------------- | -------------------- | -------------------------- |
| 객체 리터럴          | Object() 생성자 함수 | Object.prototype           |
| Object() 생성자 함수 | Object() 생성자 함수 | Object.prototype           |
| 생성자 함수          | 생성자 함수          | 생성자 함수 이름.prototype |

```javascript
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHello = function(){
    console.log('Hi! my name is ' + this.name);
  };
}

var foo = new Person('Lee', 'male');

console.dir(Person);
console.dir(foo);

console.log(foo.__proto__ === Person.prototype);                // ① true
console.log(Person.prototype.__proto__ === Object.prototype);   // ② true
console.log(Person.prototype.constructor === Person);           // ③ true
console.log(Person.__proto__ === Function.prototype);           // ④ true
console.log(Function.prototype.__proto__ === Object.prototype); // ⑤ true
```





**<생성자 함수로 생성된 객체의 프로토타입 체인>**

![constructor function prototype chaining](http://poiemaweb.com/img/constructor_function_prototype_chaining.png)



foo 객체의 프로토타입 객체 Person.prototype 객체와 Person() 생성자 함수의 프로토타입 객체인 Function.prototype의 프로토타입 객체는 Object.prototype 객체이다.

이는 객체 리터럴 방식이나 생성자 함수 방식이나 결국은 모든 객체의 부모 객체인 Object.prototype 객체에서 프로토타입 체인이 끝나기 때문이다. 이때 Object.prototype 객체를 **프로토타입 체인의 종점(End of prototype chain)**이라 한다



## 5. 프로토타입 객체의 확장

## 6.기본자료형(Primitive data type)의 확장

## 7. 프로토타입 객체의 변경

## 8.프로토타입 체인 동작 조건
