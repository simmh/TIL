# Javascript **this**

## 함수 호출 패턴에 따라 결정되는 **this**



자바스크립트는 함수 호출시var Person = function(name) {
  // 생성자 함수 코드 실행 전 -------- 1
  this.name = name;  // --------- 2
  // 생성된 함수 반환 -------------- 3
}

var me = new Person('Lee');
console.log(me.name);
function( 매개변수 ) .. arguments 객체, this 암묵적 전달 받음



## 함수 호출 패턴과 this 바인딩

자바스크립트는 함수 호출 패턴에 따라 어떤 객체를 `this`에 바인딩할 지 결정됨.
(this의 참조값이 달라진다.)



함수 호출 패턴

1. 함수 호출 패턴(Function Invocation Pattern)  `alert('Hello World!')`
2. 메소드 호출 패턴(Method Invocation Pattern) `console.log('Hello World!')`
3. 생성자 호출 패턴(Constructor Invocation Pattern) `new RegExp('\d')`
4. apply 호출 패턴(Apply Invocation Pattern) `alert.call(undefined, 'Hello World!')`





## 1. 함수 호출 패턴(Function Invocation Pattern)

전역객체(Global Object)는 모든 객체의 유일한 최상위 객체.

* Browser-side에서는 `window` (this === window // true)
* Server-side(Node.js)에서는 `global`



전역객체는 /전역 스코프(Global Scope)를 갖는 전역변수(Global variable)를 /프로퍼티로 소유한다.

글로벌 영역에 선언한 함수는 /전역객체의 프로퍼티로 접근할 수 있는 /전역 변수의 메소드이다.

```javascript
var ga = 'Global variable';

console.log(ga);
console.log(window.ga);

function foo() {
  console.log('invoked!');
}
window.foo();
```



기본적으로 `this`는 전역객체(Global object)에 바인딩된다.

전역함수, 내부함수, 메소드의 내부함수, 콜백함수의 this. 전역 객체에 바인딩 된다.

> 더글라스 크락포드는 “이것은 설계 단계의 결함으로 메소드가 내부함수를 사용하여 자신의 작업을 돕게 할 수 없다는 것을 의미한다” 라고 말한다. 



메소드 호출 패턴이든 함수 호출 패턴이든 내부함수의 this는 모두 전역객체에 바인딩된다. 
이러한 문제로 자바스크립트는 this 바인딩을 명시적으로 할 수 있는 call, apply 메소드를 제공한다.

![Function Invocation Pattern](http://poiemaweb.com/img/Function_Invocation_Pattern.png)



<내부함수의 `this`가 전역객체를 참조하는 것을 회피방법>

```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    var that = this;  // Workaround : this === obj

    console.log("foo's this: ",  this);  // obj
    console.log("foo's this.value: ",  this.value); // 100
    function bar() {
      console.log("bar's this: ",  this); // window
      console.log("bar's this.value: ", this.value); // 1

      console.log("bar's that: ",  that); // obj
      console.log("bar's that.value: ", that.value); // 100
    }
    bar();
  }
};

obj.foo();
```





## 2. 메소드 호출 패턴(Method Invocation Pattern)

함수가 객체의 프로퍼티이면 메소드 호출 패턴으로 호출된다. 이때 메소드 내부의 `this`는 해당 메소드를 소유한 객체 즉 해당 메소드를 호출한 객체에 바인딩된다.

마찬가지로 프로토타입 객체의 메소드 내부 this도 해당 메소드 호출한 객체에 바인딩 됨.

```javascript
var obj1 = {
  name: 'Lee',
  sayName: function() { //함수가 객체의 프로퍼티 - 메소드 호출 패턴
    console.log(this.name);
  }
}

var obj2 = {
  name: 'Kim'
}

obj2.sayName = obj1.sayName;

obj1.sayName(); //'lee'
obj2.sayName(); //'Kim'
```

![Method Invocation Pattern](http://poiemaweb.com/img/Method_Invocation_Pattern.png)





## 3. 생성자 호출 패턴(Constructor Invocation Pattern)

**기존 함수에 new 연산자를 붙여서 호출하면 해당 함수는 생성자 함수로 동작한다.**
일반 함수도 new 연산자를 붙여 호출하면 생성자 함수처럼 동작할 수 있다는 말.

new 연산자와 함께 생성자 함수를 호출하면 this 바인딩이 메소드나 함수 호출 때와는 다르게 동작한다.



### 3.1 생성자 함수 동작 방식

new 연산자와 함께 생성자 함수 호출시 작동 수순

1. 빈 객체 생성 및 this 바인딩
   1. 생성자 함수의 코드 실행 전 빈객체(새로 생성하는 객체) 생성
   2. 생성자 함수 내에서 사용되는 this가 빈객체 가리킴
   3. 생성된 빈 객체는 생성자 함수의 prototype 프로퍼티가 가리키는 객체를 자신의 프로토타입 객체로 설정
2. this를 통한 프로퍼티 생성
   1. 생성된 빈 객체에 this를 사용하여 동적으로 프로퍼티/메소드를 생성 가능
   2. this는 새로 생성된 객체를 가리켜 this를 통해 생성한 프로퍼티/메소드는 새로 생성된 객체에 추가됨
3. 생성된 객체 반환
   1. 반환문이 없는 경우, this에 바인딩된 새로 생성한 객체가 반환된다.
   2. . 명시적으로 this를 반환하여도 결과는 같다.
   3. 반환문이 this가 아닌 다른 객체를 명시적으로 반환하는 경우, this가 아닌 해당 객체가 반환된다.
   4. 이때 this를 반환하지 않은 함수는 생성자 함수로서의 역할을 수행하지 못한다. 
   5. 따라서 생성자 함수는 반환문을 명시적으로 사용하지 않는다.




```javascript
var Person = function(name) {
  // 생성자 함수 코드 실행 전 -------- 1
  this.name = name;  // --------- 2
  // 생성된 함수 반환 -------------- 3
}

var me = new Person('Lee');
console.log(me.name);	
```



![constructor](http://poiemaweb.com/img/constructor.png)





### 3.2 객체 리터럴 방식과 생성자 함수 방식의 차이

프로토 타입객체 [[prototype]] 차이

* 객체 리터럴 방식의 경우, 생성된 객체의 프로토 타입 객체는 Object.prototype
* 생성자 함수 방식의 경우, 생성되는 객체의 프로토타입 객체는 {{Person}}.prototype



### 3.3 생성자 함수에 new 연산자 붙이지 않고 호출할 경우

일반함수와 생성자 함수에 특별한 형식적 차이 없다.
new 연산자 붙여 호출하면 해당함수는 생성자 함수로 동작한다.

객체 생성목적 생성자 함수 new 없이 호출, 일반 함수를 new 붙여 호출 하면 오류 발생  



일반 함수 호출시 this는 전역객체에 바인딩.



생성자 함수 호출시

* new 붙여 
  * 내부 this는 생성자 함수가 생성한 빈객체에 암묵적 바인딩.
  * 내부 this는 생성자 함수에 의해 생성된 인스턴스를 가리킨다.
* new 없이
  * 내부 this.{{name}} 의 this는 전역 객체 가리킴
  * 내부 this.{{name}}의 name은 전역 변수에 바인딩
  * new와 함께 생성자 함수 호출시 암묵적으로 반환하던 this 반환하지 않음
  * 반환문 없으므로 undefined 반환.

```javascript
var Person = function(name) {
  // new없이 호출하는 경우, 전역객체에 name 프로퍼티를 추가
  this.name = name;
};

// 일반 함수로서 호출되었기 때문에 객체를 암묵적으로 생성하여 반환하지 않는다.
// 일반 함수의 this는 전역객체를 가리킨다.
var me = Person('Lee');

console.log(me); // undefined
console.log(window.name); // Lee
```



그러니 **생성자 함수명은 첫문자를 대문자로 기술하자**

이러한 위험성 회피 위해 사용 되는 패턴 (Scope-Safe Constructor )

* 대부분 라이브러리에 광범위하게 사용 됨.
* 대부분의 빌트인 생성자(Object, Regex, Array 등)는 new 연산자와 함께 호출 되었는지 확인후 적적한 값을 반환함.



```javascript
// Scope-Safe Constructor Pattern
function A(arg) {
  // 생성자 함수가 new 연산자와 함께 호출되면 함수의 선두에서 빈객체를 생성하고 this에 바인딩한다.

  /*
  this가 호출된 함수(arguments.callee, 본 예제의 경우 A)의 인스턴스가 아니면 new 연산자를 사용하지 않은 것이므로 이 경우 new와 함께 생성자 함수를 호출하여 인스턴스를 반환한다.
  arguments.callee는 호출된 함수의 이름을 나타낸다. 이 예제의 경우 A로 표기하여도 문제없이 동작하지만 특정함수의 이름과 의존성을 없애기 위해서 arguments.callee를 사용하는 것이 좋다.
  */
  if (!(this instanceof arguments.callee)) {
    return new arguments.callee(arg);
  }

  // 프로퍼티 생성과 값의 할당
  this.value = arg ? arg : 0;
}

var a = new A(100);
var b = A(10);

console.log(a.value);
console.log(b.value);
```



## 4. apply 호출 패턴(Apply Invocation Pattern)

자바스크립트 엔진의 암묵적 this 바인딩 이외에 this를 특정 객체에 명시적으로 바인딩하는 방법.

> 함수 객체의 프로토타입 객체인 Function.prototype 객체의 메소드
>
> Function.prototype.apply()
> Function.prototype.call() 





<**Function.prototype.apply()**>

```javascript
func.apply(thisArg, [argsArray])

// thisArg: 함수 내부의 this에 바인딩할 객체
// argsArray: 함수에 전달할 argument의 배열
```

* apply() 메소드를 호출하는 주체는 함수 
* apply() 메소드는 this를 특정 객체에 바인딩할 뿐 
* 본질적인 기능은 함수 호출
* apply() 메소드의 대표적인 용도는 arguments 객체와 같은 유사 배열 객체에 배열 메소드를 사용하는 경우

```javascript
var Person = function (name) {
  this.name = name;
};

var foo = {};

// apply 메소드는 생성자함수 Person을 호출한다. 이때 this에 객체 foo를 바인딩한다.
//빈 객체 foo를 apply() 메소드의 첫번째 매개변수에, argument의 배열을 두번째 매개변수에 전달하면서 Person 함수를 호출.
Person.apply(foo, ['name']);

//Person 함수의 this는 foo 객체가 된다.
//Person 함수는 this의 name 프로퍼티에 매개변수 name에 할당된 인수를 할당.

console.log(foo); // { name: 'name' } //name 프로퍼티가 동적 추가되고 값이 할당
```



[ apply() 메소드 활용  - 유사 배열 객체에 배열 메소드를 사용하는 경우 ]

arguments 객체는 배열이 아니기 때문에 slice() 같은 배열의 메소드를 사용할 수 없기에 apply() 메소드 이용

```javascript
function convertArgsToArray() {
  console.log(arguments);

  // arguments 객체를 배열로 변환
  // slice: 배열의 특정 부분에 대한 복사본을 생성한다.
  var arr = Array.prototype.slice.apply(arguments); // arguments.slice
  // var arr = [].slice.apply(arguments);

  console.log(arr);
  return arr;
}

convertArgsToArray(1, 2, 3);
```

`Array.prototype.slice.apply(arguments)` == `arguments.slice()`

“Array.prototype.slice() 메소드를 호출하라. 단 this는 arguments 객체로 바인딩하라”
결국 Array.prototype.slice() 메소드를 arguments 객체 자신의 메소드인 것처럼 `arguments.slice()`와 같은 형태로 호출



![apply](http://poiemaweb.com/img/apply.png)



------

<**Function.prototype.call()** > 
call() 메소드의 경우 ,
apply()와 기능은 같지만 apply()의 두번째 인자에서 배열 형태로 넘긴 것을 각각 하나의 인자로 넘긴다.

```javascript
Person.apply(foo, [1, 2, 3]);
Person.call(foo, 1, 2, 3);
```

apply()와 call() 메소드는 콜백 함수의 this를 위해서 사용되기도 한다.



```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.doSomething = function(callback) {
  if(typeof callback == 'function') {
    // --------- 1
    callback();
  }
};

function foo() {
  console.log(this.name); // --------- 2
}

var p = new Person('Lee');
p.doSomething(foo);  // undefined

```

1의 시점에서 this는 Person 객체이다. 그러나 2의 시점에서 this는 전역 객체 window를 가리킨다. 콜백함수를 호출하는 외부 함수 내부의 this와 콜백함수 내부의 this가 상이하기 때문에 문맥상 문제가 발생한다. 따라서 콜백함수 내부의 this를 콜백함수를 호출하는 함수 내부의 this와 일치시켜 주어야 하는 번거로움이 발생한다.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.doSomething = function(callback) {
  if(typeof callback == 'function') {
    callback.call(this);
  }
};

function foo() {
  console.log(this.name);
}

var p = new Person('Lee');
p.doSomething(foo);  // 'Lee'
```





<이 외..>
ES5에 추가된 [Function.prototype.bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)를 사용하는 방법.
ES6에서 새롭게 제공되는 [Arrow function](http://poiemaweb.com/es6-arrow-function)을 사용하면 call() 메소드를 사용하지 않아도 된다.

------

요약

1. 객체의 메소드 안에서의 this

   해당 메소드를 호출한 객체에 바인딩.

```javascript
var obj = {  
  sayName : function() {
    console.log(this.name);
  }
};

var kim = obj;
kim.name = "kim";
kim.sayName();   // "kim"

var lee = obj;
lee.name = "lee";
lee.sayName();   // "lee"
```



2. 함수내의 this

   함수내의 this는 전역객체(window)를 가리킴

```javascript
var val = "Hello";

var func = function() {
  console.log(this.val);

};
func();   // "Hello"
console.log(this.val);  // "Hello"
console.log(window.val);  //  "Hello"
console.log(this === window);  // true  
```



3. 생성자 함수내의 this

   생성자 함수내의 this는 new로 생성자 함수를 생성한 객체에 바인딩 됨.

```javascript
var Person = function(name) {
	this.name = name;
};

var kim = new Person('kim');
console.log(kim.name); //kim

var lee = new Person('lee');
console.log(lee.name); //lee
```

new 사용하지 않고 호출한다면

```javascript
var park = Person('park');
console.log(park.name); //"TypeError: Cannot read property 'name' of undefined
//성자 함수 호출의 경우는 this 는 새로 생성된 빈객체에 바인딩된다.
```



