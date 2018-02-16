# Javascript Syntax Basics

## 구문 (Statement)

- 각각의 명령을 statement(구문)이라 하며 statement가 실행되면 무슨 일인가가 일어나게 된다.
- 구문은 값(Value), 연산자(Operator), 표현식(Expression), 키워드(Keyword), 주석(Comment)으로 구성되며 세미콜론( ; )으로 끝나야 한다.
- 구문은 코드 블록(code block, {…})으로 그룹화할 수 있다. 그룹화의 목적은 함께 실행되어져야 하는 구문을 정의하기 위함이다.

## 표현식 (Expression)

## 변수 (Variable)

## 값 (Value)

- 기본 자료형 (primitive data type)
  - `Boolean`
  - `null`
  - `undefined`
  - `Number`
  - `String`
  - `Symbol` (New in ECMAScript 6)
- `Object`

## 연산자 (Operator)

## 키워드 (keyword)

## 주석 (Comment)



# Javascript Data type & Variable

## Data Type (자료형)

### 기본자료형 (Primitive Data Type)

#### Boolean

### null

### undefined

### Number

### String

### Symbol



# Javascript **Operator** 연산자

연산자(Operators)는 하나 혹은 그 이상의 값을 **하나의 값으로 만들 때** 사용한다.



# 산술 연산자 (Arithmetic Operators)

`+ 연산자`는 덧셈 연산과 문자열 연결 연산을 수행한다.

- 연산 대상이 모두 숫자인 경우 : 덧셈 연산
- 그 외의 경우 : 문자열 연결 연산

z = x++;    // 5 선대입후증가
z = ++x;    // 7 선증가후대입
z = x--;    // 7 선대입후감소
z = --x;    // 5 선감소후대입

# 대입 연산자 (Assignment Operators)

| Operator | Example | Same As   |
| -------- | ------- | --------- |
| =        | x = y   | x = y     |
| +=       | x += y  | x = x + y |
| -=       | x -= y  | x = x - y |
| *=       | x *= y  | x = x * y |
| /=       | x /= y  | x = x / y |
| %=       | x %= y  | x = x % y |

var x;

x = 10;   // 10
x += 5;   // 15
x -= 5;   // 10
x *= 5;   // 50
x /= 5;   // 10
x %= 5;   // 0



# 비교 연산자 (Comparison Operators)

// 삼항연산자(ternary operator)
// 조건 ? 조건이 ture일때 반환할 값 : 조건이 false일때 반환할 값
var condition = true;
var result = condition ? 'true' : 'false';
console.log(result); // 'true'

// id의 길이가 INPUT_ID_MIN_LEN보다 작으면 에러 메시지를 출력한다.
var id = 'lee';
var INPUT_ID_MIN_LEN = 5;
var errMsg = id.length < INPUT_ID_MIN_LEN ? '아이디는 5자리 이상으로 입력하세요' : '성공';
console.log(errMsg); // '아이디는 5자리 이상으로 입력하세요'

# 논리 연산자 (Logical Operators)

// ! (논리 부정) 연산자
var n1 = !true;  // false
var n2 = !false; // true
var n3 = !'Cat'; // false



# 단축 평가 (Short-Circuit Evaluation)

논리연산자가 Boolean 값과 함께 사용되지 않을 경우, Boolean 값을 반환하지 않을 수 있다. 이는 논리 연산자가 피연산자 중 하나를 반환하기 때문이다. 논리연산자는 다음의 규칙을 따라서 “단축 평가”로 검사된다.

| 평가식                 | 평가 결과    |
| ------------------- | -------- |
| true \|\| anything  | true     |
| false \|\| anything | anything |
| true && anything    | anything |
| false && anything   | false    |

# 타입 연산자 (Type Operators)

| Operator   | Description                              |
| ---------- | ---------------------------------------- |
| typeof     | 피연산자의 데이터 타입(자료형)을 문자열로 반환한다. null과 배열의 경우 object, 함수의 경우 function를 반환하는 것에 유의하여야 한다. |
| instanceof | 객체가 동일 객체형의 인스턴스이면 `true`를 반환한다.         |

#  !!

`!!`의 역할은 피연산자를 불린값으로 변환하는 것이다.

```
console.log(!!1);         // true
console.log(!!0);         // false
console.log(!!'string');  // true
console.log(!!'');        // false
console.log(!!null);      // false
console.log(!!undefined); // false
console.log(!!{});        // true
console.log(!![]);        // true

```

객체(배열 포함)의 경우 빈 객체라도 존재하기만하면 true로 변환된다.

객체의 존재 확인 후 그 결과를 반환해야 하는 경우, !!를 사용하면 강제로 피연산자를 boolean으로 형 변환 할 수 있다.

```
var obj;
console.log(!!obj); // false

obj = {};
console.log(!!obj); // true
```


# # Reference

http://poiemaweb.com/js-syntax-basics