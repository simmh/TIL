# Javascript **Standard Built-in Objects**



## 1. 전역 객체(Global Object)



### 1.1 전역 프로퍼티(Global property)

 간단한 값이 대부분. (프로퍼티, 메소드 없음)

#### Infinity

window.Infinity  = Infinity
console.log(typeof Infinity); // number 숫자값



#### NaN

숫자값 NaN
NaN === Number.NaN
console.log(typeof NaN);    // number 숫자값



#### undefined

window.undefined
window['undefined'] = undefined // 기본 자료형 값
console.log(typeof undefined); // undefined



### 1.2 전역 함수(Global function)



#### eval()

매개변수에 전달된 문자열 구문 또는 표현식을 평가 또는 실행. 
사용자 입력 컨텐트 실행시 보안에 매우 취약.



#### isFinite()

유한수인지 검사

```javascript
isFinite()  // false
isFinite(undefined);  // false
isFinite(Infinity);  // false
(isFinite(NaN);       // false
isFinite('Hello');   // false
isFinite('2005/12/12');   // false

isFinite('');        // true
isFinite(0);         // true
isFinite(2e64);      // true
isFinite(null);      // true: null->0

Number(null)  // 0
Boolean(null) // false
```



#### isNaN()

```javascript
// 숫자 아님 판명
isNaN(NaN)       // true
isNaN(undefined) // true: undefined -> NaN
isNaN({})        // true: {} -> NaN
isNaN('blabla')  // true: 'blabla' -> NaN

isNaN(true)      // false: true -> 1
isNaN(null)      // false: null -> 0
isNaN(37)        // false

//숫자 판명
// strings
isNaN('37')      // false: '37' -> 37
isNaN('37.37')   // false: '37.37' -> 37.37
isNaN('')        // false: '' -> 0
isNaN(' ')       // false: ' ' -> 0

// dates
isNaN(new Date())             // false: new Date() -> Number
isNaN(new Date().toString())  // true:  String -> NaN
```



#### parseFloat()

```javascript
parseFloat('3.14');     // 3.14 -> 소숫점 숫자
parseFloat('10.00');    // 10 -> 00버림
parseFloat('34 45 66'); // 34 -> 앞 숫자만
parseFloat(' 60 ');     // 60
parseFloat('40 years'); // 40
parseFloat('He was 40') // NaN
```



#### parseInt()

parseInt(string, radix); // string 변환 할 문자 , radix 진법 기수



#### encodeURI() / decodeURI()

```javascript
var enc = encodeURI(uri);
// http://example.com?name=%EC%9D%B4%EC%9B%85%EB%AA%A8&job=programmer&teacher
var dec = decodeURI(enc);
// http://example.com?name=이웅모&job=programmer&teacher
```



## 2. 표준 빌트인 객체(Standard Built-in Objects / Global objects)

#### Object

#### Function

#### Boolean

#### Number

#### Math

#### Date

#### String

#### RegExp

#### Array

#### Error

#### Symbol



## 3. 기본자료형과 래퍼객체(Wrapper Object)



## Reference

http://poiemaweb.com/js-standard-built-in-objects