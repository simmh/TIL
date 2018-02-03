#  5.7 Javascript Object 객체

## 1. 객체(Object)란?

자바스크립트는 객체(object)기반의 스크립트 언어이며 거의 "모든 것은" 객체이다.
기본자료형(primitives)을 제외한 나머지 값들(함수,배열, 정규 표현식 등)은 모두 객체이다.

객체는 데이터와 그 데이터에 관련된 동작(절차, 방법, 기능)을 모두 포함할 수 있는 개념적 존재.
키와 값으로 구성된 프로퍼티(property)와 메소드(method)를 포함하고 있는 독립적 주체.

객체는 데이터를 한 곳에 모으고 구조화 하는데 유용하다.
객체 하나는 다른 객체를 포함 할 수 있어 그래프, 트리 같은 자료 구조 쉽게 표현



자바스크립트 내장 객체 타입.
객체의 유연한 성질 때문에 커스텀 데이터 타입을 만들 때 많이 사용한다

Array

Date

RegExp

Map과 WeakMap

Set과 WeakSet

이외 원시 타입 숫자와 문자열, 불리언에 각각 대응하는 객체 타입 Number, String Boolean.
대응하는 객체에 실제 값이 저장되지는 않는다. 원시값에 기능을 제공하는 역할



### 1.1 프로퍼티(Property)

프로퍼티란?  이름(name): "값(value)" 의 쌍
객체는 이런 프로퍼티 포함 컨테이너 { }

* 프로퍼티 이름 : 빈 문자열을 포함하는 문자열과 숫자 {"property name 123" : null}
* 프로퍼티 값: undefined를 제외한 모든 값 



### 1.2 메소드(Method)

객체에 제한되어 있는 함수.
프로퍼티 값이 함수일 경우, 일반 함수와 같으나 이름을 구분을 위해 메소드라 칭한다.



## 2. 객체 생성 방법

### 2.1 객체 리터럴

중괄호 { }사용. 
빈 중괄호로 빈객체 생성.  
프로퍼티 이름(Property name) : 프로퍼티 값(Property value) 넣고 객체 생성 가능.



## 2.2 Object() 생성자 함수

new 연산자와 Object() 생성자 함수를 사용하여 빈객체 생성. 
var person = new Object();

프로퍼티에 새로운 값할당 -> 프로퍼티 값 갱신

없는 프로퍼티에 값 할당 -> 프로퍼티 추가 후 값 할당

**객체 리터럴 방식으로 생성된 객체는 결국 내장(Built-in) 함수인 Object() 생성자 함수로 객체를 생성하는 것을 단순화 시킨 short-hand(축약법)이다.** 



```
//객체 리터럴 생성 법
var emptyObject = {};
console.log(typeof emptyObject); // object

var person = {
  name: 'Lee',
  gender: 'male',
  sayHello: function () {
    console.log('Hi! My name is ' + this.name);
  }
};

//=======================================

// new연산자 Object() 생성자 함수 사용 생성법
var person = new Object(); //빈 객체의 생성

person.name = 'Lee'; // 프로퍼티 추가
person.gender = 'male';
person.sayHello = function () {
  console.log('Hi! My name is ' + this.name);
};

console.log(typeof person); // object
console.log(person); // { name: 'Lee', gender: 'male', sayHello: [Function] }

person.sayHello(); // Hi! My name is Lee

//======================================

// 생성자 함수
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHello = function(){
    console.log('Hi! My name is ' + this.name);
  };
}

// 인스턴스의 생성
var person1 = new Person('Lee', 'male');
var person2 = new Person('Kim', 'female');

console.log('person1: ', typeof person1);
console.log('person2: ', typeof person2);
console.log('person1: ', person1);
console.log('person2: ', person2);

person1.sayHello();
person2.sayHello();
```



### 2.3 생성자 함수

객체 리터럴 방식, **Object() 생성자 함수** 방식 객체 생성은 불편.
템플릿(클래스)처럼 구성 동일 객체 여러게 간편 생성.

* 이름은 대문자로 시작. 생성자 함수임을 인식하게 function Person(매변1, 매변2) {}
* 프로퍼티 또는 메소드명 앞에 this.는 생성자 함수가 생성할 **인스턴스(instance)**를 가르킴
* this에 연결(바인딩)되어 있는 프로퍼티&메소드는 public(외부 참조 가능)하다.
* 생성자 함수 내에 선언된 일반 변수는 private(외부 참조 불가)하다. 함수 내부서만 접근 가능

생성자 함수는 다른 형식이 아니라기존 함수 생성 방식에 new 연산자 붙여 호출 한 것. 
그러니 생성자 함수는 함수명 첫문자 대문자는 생성자함수로 구별

new 연산자와 함께 함수를 호출하면 `this` 바인딩이 다르게 동작한다. ?? [생성자 호출 패턴](http://poiemaweb.com/js-this#3-%EC%83%9D%EC%84%B1%EC%9E%90-%ED%98%B8%EC%B6%9C-%ED%8C%A8%ED%84%B4constructor-invocation-pattern)

일반 함수에 new 연산자 붙여 호출시?

```
function Person(name, gender) {
  var married = true;         // private
  this.name = name;           // public
  this.gender = gender;       // public
  this.sayHello = function(){ // public
    console.log('Hi! My name is ' + this.name);
  };
}

var person = new Person('Lee', 'male');

console.log(typeof person); // object
console.log(person); // Person { name: 'Lee', gender: 'male', sayHello: [Function] }

console.log(person.gender);  // 'male'
console.log(person.married); // undefined
```



## 3. 객체 프로퍼티 접근

### 3.1 프로퍼티 이름

* 문자열로 작성(빈 문자열 포함)
* 숫자로 작성 가능. 암묵정 형변환 되어 문자열 됨.
* 사용가능한 유효한 이름경후 ''사용 생략 가능하나, 아니면 ''사용하여 써줌
* first-name 같은 '-' 연산자 표현식 이름에 주의
* 예약어를  프로퍼티이름으로 사용해도 에러 없으나, 예상치 못한 상황 발생 가능성 up.


```
//예약어
abstract  arguments boolean break byte
case  catch char  class*  const
continue  debugger  default delete  do
double  else  enum* eval  export*
extends*  false final finally float
for function  goto  if  implements
import* in  instanceof  int interface
let long  native  new null
package private protected public  return
short static  super*  switch  synchronized
this  throw throws  transient true
try typeof  var void  volatile
while with  yield
// *는 ES6에서 추가된 예약어
```



### 3.2 프로퍼티 값 읽기

프로퍼티(또는 멤버member) 접근 방법 

* 마침표(.) 표기법. (멤버 접근 연산자 member access operator)
*  대활호 ([])표기법. (계산된 멤버 접근 연산자 computed member access operator)
  * **대괄호 내에 들어가는 프로퍼티 이름은 반드시 문자열이어야 한다.**



* 프로퍼티 값은 undefined 제외 모든 값, 표현식 가능. 
* 객체에 존재하지 않는 프로퍼티 참조하면 **undefiend** 반환

```
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
  1: 10
};

console.log(person);

console.log(person.first-name);    // NaN: undefined-undefined
console.log(person[first-name]);   // ReferenceError: first is not defined
console.log(person['first-name']); // 'Ung-mo'

console.log(person.gender);    // 'male'
console.log(person[gender]);   // ReferenceError: gender is not defined
console.log(person['gender']); // 'male'

console.log(person['1']); // 10
console.log(person[1]);   // 10 : person[1] -> person['1'] //문자로 변환 됨
console.log(person.1);    // SyntaxError ???
```



### 3.4 프로퍼티 동적 생석

```
person.age = 20 //person 오브젝트에 없던 age 프로퍼티와 20 값 동적 생성
```



### 3.5 프로퍼티 삭제

```
delete person.gender // gender 프로퍼티 삭제
delete person // 삭제 안되고 false 리턴
```



3. 6 for-in 문

자바스크립트 for-in문은 문자열 키 순회하기 위한 문법. 배열에는 사용하지 않는게 좋음.

1. 객체의 경우, 프로퍼티의 순서가 보장되지 않는다. 그 이유는 원래 객체의 프로퍼티에는 순서가 없기 때문이다. 배열은 순서를 의식하는 데이터 구조이지만 객체와 마찬가지로 순서를 보장하지 않는다.
2. 배열 요소들만을 순회하지 않는다.



## 4. Pass-by-reference

object type을 객체형 또는 참조형이라 한다. 
객체의 모든 연산이 참조값으로 처리됨을 의미.
객체는 프로퍼티 변경, 추가, 삭제 가능하므로 변경가능 값(mutable)한 값이라 한다.

object type의 값은 동적으로 변화 할수 있으므로 메모리 공간 확보시 예측 불가.
런타임에 메모리 공간 확보, 메모리의 힙 영역(Heap segment)에 저장 됨.

```
// Pass-by-reference

// 변수 foo는 생성된 객체의 참조값(address) 저장하고 있다
var foo = {
  val: 10
}

var bar = foo; //bar 변수에 foo의 값(참조값) 저장
console.log(foo.val, bar.val); // 10 10 
console.log(foo === bar);      // true

bar.val = 20;
console.log(foo.val, bar.val); // 20 20
console.log(foo === bar);      // true
```



당연히 같은 프로퍼티 명에 값이 같다고 같은 데이터 아니다. 어드레스 동일 x

```
var foo = { val: 10 };
var bar = { val: 10 };

console.log(foo.val, bar.val); // 10 10
console.log(foo === bar);      // false

```



객체 {}

```
var a = {}, b = {}, c = {}; // a, b, c는 각각 다른 빈 객체를 참조
console.log(a === b, a === c, b === c); // false false false

a = b = c = {}; // a, b, c는 모두 같은 빈 객체를 참조
console.log(a === b, a === c, b === c); // true true true
```





## 6. 객체의 분류

* Object
  * [Built-in Object(내장 객체)](http://poiemaweb.com/js-built-in-object)
    웹페이지 등을 표현하기 위한 공통의 기능을 제공.
    웹페이지가 브라우저에 의해 로드되자마자 별다른 행위없이 바로 사용이 가능.
  * Host Object(사용자 정의 객체)
    사용자가 생성한 객체 들. 
    constructor 혹은 객체리터럴을 통해 사용자가 객체를 정의하고 확장시킨 것들이기 때문에
    Built-in Object 와 Native Object가 구성된 이후에 구성된다.







![object](http://poiemaweb.com/img/object.png)