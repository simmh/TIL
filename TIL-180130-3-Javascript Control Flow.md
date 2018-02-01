# Javascript **Control Flow**

## 제어문

제어문(Control flow statement)은 조건에 따른 명령 실행(조건문)이나 반복 실행(반복문)이 필요할 때 사용된다.

일반적으로 코드는 위에서 아래 방향으로 순차적 실행을 하지만 실행 순서를 변경하거나 조건에 따라 실행 여부를 결정하기도 하고 반복할 수도 있다.

# 1. 블록 구문(Block statement)

블록 구문(Block statement)는 구문들의 집합으로 {}중괄호로 그 범위를 정한다. 

일반적 사용처 

* 함수 
* 객체리터럴
* 흐름 제어 구문(control flow statement) (e.g. if, for, while)



# 2. 조건문(Conditional statement)



## 2.1 if 문

## 2.2 switch 문

# 3. 반복문(Loop)

## 3.1 for 문

## 3.2 while 문

## 3.3 do while문

## 3.4 continue

# 4. 평가(Evaluating)
흐름제어를 위해 조건식을 평가하여 논리적 참, 거짓 구별


## 4.1 암묵적 강제 형 변환 (Type coercion)
자바스크립트는 context(문맥)을 고려하여 자료형을 암묵적으로 강제 변환하여 작업을 완료할 수 있다.
자바스크립트는 조건식에서 0,1 결과 값을 불리언 타입으로 변환시킨다.
의도하지 않은 값을 만들어낼 수 있어 주의가 필요하다.

console.log('1' > 0);            // true  //'1' 을 숫자 1로 변환하고 비교한다.
console.log(1 + '2');            // '12' 
console.log(2 - '1');            // 1 //산술연산자 - 때문에 계산한다.
console.log('10' == 10);         // true
console.log('10' === 10);        // false
console.log(undefined == null);  // true
console.log(undefined === null); // false

## 4.2 Type Conversion Table
| Original Value    | Converted to Number | Converted to String | Converted to Boolean |
| ----------------- | ------------------- | ------------------- | -------------------- |
| false             | **0**               | ‘false’             | false                |
| true              | **1**               | ‘true’              | true                 |
| 0                 | 0                   | ‘0’                 | **false**            |
| 1                 | 1                   | ‘1’                 | true                 |
| ‘0’               | **0**               | ‘0’                 | **true**             |
| ‘1’               | **1**               | ‘1’                 | true                 |
| NaN               | NaN                 | ‘NaN’               | **false**            |
| Infinity          | Infinity            | ‘Infinity’          | true                 |
| -Infinity         | -Infinity           | ‘-Infinity’         | true                 |
| ’’                | **0**               | ’’                  | **false**            |
| ‘10’              | 10                  | ‘10’                | true                 |
| ‘ten’             | NaN                 | ‘ten’               | true                 |
| [ ]               | **0**               | ’’                  | true                 |
| [10]              | **10**              | ‘10’                | true                 |
| [10, 20]          | NaN                 | ‘10,20’             | true                 |
| [‘ten’]           | NaN                 | ‘ten’               | true                 |
| [‘ten’, ‘twenty’] | NaN                 | ‘ten, twenty’       | true                 |
| function(){}      | NaN                 | ‘function(){}’      | true                 |
| { }               | NaN                 | ‘[object Object]’   | true                 |
| null              | **0**               | ‘null’              | **false**            |
| undefined         | **NaN**             | ‘undefined’         | **false**            |

var x = false;

// 변수 x의 값을 숫자 타입으로 변환
console.log('Number : ' + Number(x));  // 0
// 변수 x의 값을 문자열 타입으로 변환
console.log('String : ' + String(x));  // 'false'
// 변수 x의 값을 불리언 타입으로 변환
console.log('Boolean: ' + Boolean(x)); // false


”+” 단항 연산자는 대부분의 값을 **숫자형**으로 변환할 수 있다.

console.log(+10);     // 10
console.log(+'10');   // 10
console.log(-'10');   // -10
console.log(+true);   // 1
console.log(+false);  // 0
console.log(+null);   // 0
console.log(+undefined); // NaN
console.log(+NaN);    // NaN

## 4.3 Data type conversion
단항 연산자 쓴다
*1을 해도 된다.
```
var val = '123';
console.log(typeof val + ': ' + val); // string: 123

// sting -> number
val = +val; // "+": 단항 연산자(unary operator)
// val = val * 1;
// val = parseInt(val);
// val = Number(val); //왠만하면 쓰지 말라.
console.log(typeof val + ': ' + val); // number: 123

// number -> sting
val = val + '';
// val = String(val); //비추
// val = val.toString();
console.log(typeof val + ': ' + val); // string: 123
```

## 4.4 Truthy & Falsy values
Boolean context에서 false 로 평가된다.
이들을 Falsy value라 한다.
Falsy value 이외의 값들(object 포함)은 모두 true로 평가된다. 이들을 Truthy value라 한다.

* false
* undefined
* null
* 0
* NaN (Not a Number)
* '' (빈문자열)
* ​
## 4.5 Checking equality
* 두 값이 같은 값인지 비교할 때에 동등 연산자(==, !=)보다 일치 연산자(===, !==)를 사용
* 암묵적으로 변환된 값만을 비교말고  자료형까지 비교하여 정확한 결과 얻자.

## 4.6 Checking existence
```
// DOM에서 특정 요소를 취득
var elem = document.getElementById('header'); // getElementById 실패시 null

if (elem) {
  // 요소가 존재함(요소 취득 성공) : 필요한 작업을 수행
} else {
  // 요소가 존재하지 않음(요소 취득 실패) : 에러 처리
}
```

아래 예는 위의 예와는 다른 의미이다. 객체의 존재는 truthy value로 취급지만 boolean 값 true와 같지는 않다.
```
// DOM에서 특정 요소를 취득
var elem = document.getElementById('header');

// 변수 elem의 값이 true인지 평가한다.
// 변수 elem의 값은 null 또는 HTMLElement를 상속받은 객체의 인스턴스
if (elem == true) // false
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NjAwMDgwMzRdfQ==
-->