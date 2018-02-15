# Javascript **Scope**

# 변수에의 접근성과 생존기간(life-cycle)



**Scope란?** 
변수에의 접근성과 생존기간(life-cycle)을 의미한다. 
변수가 가지고 있는 참조 범위를 의미한다.



**자바스크립트의 Scope 종류**

* **전역 Scope (Global scope)** 
  * 코드 어디에서든지 참조 가능.
  * 전역 scope를 갖는 변수: **전역 변수 (Global variable)** -
* **지역 Scope (Local scope or Function-level scope)**
  * 정의된 함수 내에서만 참조 가능.
  * 지역 Scope를 갖는 변수 :  **지역 변수 (Local variable)**
  * 지역(함수 내부)에서 선언된 지역 변수는 그 지역과 그 지역의 하부 지역에서만 참조할 수 있다.**



자바스크립트는 **function-level scope**를 사용한다.

*  function-level scope: 함수 코드 블럭 내에서 선언된 변수는 함수 코드 블럭 내에서만 유효하고 함수 외부에서는 유효하지 않다.  “유효하다”라는 것은 “참조(접근)할 수 있다”라는 뜻.
*  ECMAScript 6에서 도입된 [let](http://poiemaweb.com/es6-block-scope) keyword를 사용하면 **block-level scope**를 사용할 수 있다.



## 1. Global scope

글로벌 영역에 변수를 선언하면 이 변수는 어느 곳에서든지 참조할 수 있는 global scope를 갖는 전역 변수가 된다. 
전역 변수는 [전역 객체(Global Object)](http://poiemaweb.com/js-standard-built-in-objects#1-%EC%A0%84%EC%97%AD-%EA%B0%9D%EC%B2%B4global-object) `window`의 프로퍼티이다.

자바스크립트는 타 언어와는 달리 특별한 시작점(Entry point)이 없어서 위 코드와 같이 글로벌 영역에 변수나 함수를 선언하기 쉽다.

자바스크립트는 다른 C-family language와는 달리 특별한 시작점이 없으며 코드가 나타나는 즉시 해석되고 실행된다. 따라서 글로벌 영역에 변수를 선언하기 쉬우며 이것는 전역 변수를 남발하게 하는 문제를 야기시킨다.



## 2. Non block-level scope

자바스크립트는 block-level scope를 사용하지 않으므로 **function 밖에서 선언된 변수는 코드 블럭 내에서 선언되었다할지라도 모두 global scope**을 갖게된다.



## 3. Function scope

자바스크립트는 function-level scope를 사용한다. 즉 함수 내에서 선언된 매개변수와 변수는 함수 외부에서는 유효하지 않다.

함수 내 지역 영역에서는 전역과 지역 변수 모두 참조 가능하나 변수명이 중복된 경우, 지역변수를 우선하여 참조한다. 



```javascript
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x); // local

  function bar() {  // 내부함수
    console.log(x); // ? local
  }

  bar();
 //bar에서 참조하는 변수 x는 함수 foo에서 선언된 지역변수이다.
 // 실행 컨텍스트의 스코프 체인에 의해 참조 순위에서 전역변수 x가 뒤로 밀렸기 때문  
}
foo();
console.log(x); // ? global
```

내부함수는 자신을 포함하고 있는 외부함수의 변수에 접근할 수 있다. **클로저 관련

```javascript
// 전역변수,내부에서 상위함수 참조할수 있어 접근/변경 가능
// 위치 바꿔 실험해 보기
var x = 10;

function foo(){
  var x = 100;
  console.log(x);

  function bar(){   // 내부함수
    x = 1000;
    console.log(x); // ?
  }

  bar();
}
foo();
console.log(x); // ?
```



```javascript
//중첩 scope는 가장 인접한 지역을 우선하여 참조한다.
var foo = function ( ) {

  var a = 3, b = 5;

  var bar = function ( ) {
    var b = 7, c = 11;

// 이 시점에서 a는 3, b는 7, c는 11
      
    a += b + c;

// 이 시점에서 a는 21, b는 7, c는 11

  };

// 이 시점에서 a는 3, b는 5, c는 not defined

  bar( );

// 이 시점에서 a는 21, b는 5

};
```



## 4. 암묵적 전역 (implied globals)

선언되지 않은 변수에 값을 할당시 상위 지역(아래 예제의 경우 전역)에서 변수 x를 찾고 존재하지 않으면 변수 x를 암묵적으로 전역변수로 선언한다.



## 5. Lexical scoping (Static scoping)

자바스크립트는 함수가 선언된 시점에서의 유효범위를 갖는다.

```javascript
var i = 5;

function foo() {
  var i = 10;
  bar();
}

function bar() { // 선언된 시점에서의 scope를 갖는다!
  console.log(i);
}

foo(); // ? 5 ??
```



## 6. 변수명의 중복

자바스크립트는 HTML에서  2개 이상의 자바스크립트 파일을 로드시  전역변수의 변수명 중복을 허용며 에러를 발생시키지 않으므로 주의한다.

**전역변수를 반드시 사용하여야 할 이유를 찾지 못한다면 지역변수를 사용하여야 한다. 변수의 범위인 스코프는 좁을수록 좋다.**

코드가 길어지면 변수명의 중복이 발생하기 쉬워 예기치 못한 이상 동작의 원인이 되기 쉬우며, 전역변수는 지역변수보다 탐색에 걸리는 시간이 더 길다.(속도면에서 그리 큰 차이는 없지만 분명히 느리다.)



## 7. 최소한의 전역변수 사용

애플리케이션에서 전역변수 사용을 위해 전역변수 객체 하나를 만들어 사용하는 방법 
(더글라스 크락포드의 제안)

```javascript
var MYAPP = {};

MYAPP.student = {
  name: 'Lee',
  gender: 'male'
};

console.log(MYAPP.student.name);
```



## 8. 즉시실행함수를 이용한 전역변수 사용 억제

즉시 실행 함수(IIFE, Immediately-Invoked Function Expression)는 즉시 실행되고 그 후 전역에서 바로 사라진다.

```javascript
(function () {
  var MYAPP = {};

  MYAPP.student = {
    name: 'Lee',
    gender: 'male'
  };

  console.log(MYAPP.student.name);
}());

console.log(MYAPP.student.name);
```



