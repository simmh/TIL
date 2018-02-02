## 1. 산술 연산자 (Arithmetic Operators)

Operator:

```
+  -  *  /  %  ++  --
```

```
var x = 5;
var y = 2;
var z;

z = x++;    // 5 선대입후증가
z = ++x;    // 7 선증가후대입
z = x--;    // 7 선대입후감소
z = --x;    // 5 선감소후대입
```

`+ 연산자`는 덧셈 연산과 문자열 연결 연산을 수행한다.

- 연산 대상이 모두 숫자인 경우 : 덧셈 연산
- 그 외의 경우 : 문자열 연결 연산



## 2. 대입 연산자 (Assignment Operators)

| Operator | Example | Same As   |
| -------- | ------- | --------- |
| =        | x = y   | x = y     |
| +=       | x += y  | x = x + y |
| -=       | x -= y  | x = x - y |
| *=       | x *= y  | x = x * y |
| /=       | x /= y  | x = x / y |
| %=       | x %= y  | x = x % y |

```
var x;

x = 10;   // 10
x += 5;   // 15
x -= 5;   // 10
x *= 5;   // 50
x /= 5;   // 10
x %= 5;   // 0
```



## 3. 비교 연산자 (Comparison Operators)

| Operator | Description                              |
| -------- | ---------------------------------------- |
| ==       | 동등비교 (loose equality) 형변환 후, 비교한다.       |
| ===      | 일치비교 (strict equality) 타입까지 일치하여야 true를 반환한다. |
| !=       | 부등비교                                     |
| !==      | 불일치비교                                    |
| >        | 관계비교                                     |
| <        | 관계비교                                     |
| >=       | 관계비교                                     |
| <=       | 관계비교                                     |
| ?        | 삼항 연산자                                   |

```
// 삼항연산자(ternary operator)
// 조건 ? 조건이 ture일때 반환할 값 : 조건이 false일때 반환할 값
var condition = true;
var result = condition ? 'true' : 'false';
console.log(result); // 'true'
```



## 4. 논리 연산자 (Logical Operators)

논리 연산자는 Boolean 값과 함께 사용하여 Boolean 값을 반환하는 것이 일반적이다. 사실 논리 연산자는 피연산자 중 하나를 반환한다.

| Operator | Description |
| -------- | ----------- |
| \|\|     | or          |
| &&       | and         |
| !        | not         |

```
// || (논리 합) 연산자
var o1 =  true || true;     // t || t returns true
var o2 = false || true;     // f || t returns true
var o3 =  true || false;    // t || f returns true
var o4 = false || (3 == 4); // f || f returns false

// && (논리곱) 연산자
var a1 =  true && true;     // t && t returns true
var a2 =  true && false;    // t && f returns false
var a3 = false && true;     // f && t returns false
var a4 = false && (3 == 4); // f && f returns false

// ! (논리 부정) 연산자
var n1 = !true;  // false
var n2 = !false; // true
var n3 = !'Cat'; // false
```



## 5. 단축 평가 (Short-Circuit Evaluation)

논리연산자가 Boolean 값과 함께 사용되지 않을 경우, Boolean 값을 반환하지 않을 수 있다. 이는 논리 연산자가 피연산자 중 하나를 반환하기 때문이다. 논리연산자는 다음의 규칙을 따라서 “단축 평가”로 검사된다.

| 평가식                 | 평가 결과    |
| ------------------- | -------- |
| true \|\| anything  | true     |
| false \|\| anything | anything |
| true && anything    | anything |
| false && anything   | false    |

Boolean값으로 평가하기 위해 참조하여야 할 곳까지 진행한 후, 평가를 중지하게된 계기가 된 값을 반환한다.

```
var foo = 'Cat' && 'Dog'  // t && t returns 'Dog'
var foo = false && 'Cat'  // f && t returns false
var foo = 'Cat' || 'Dog'  // t || t returns 'Cat'
```



```
// || (논리 합) 연산자
var o1 = 'Cat' || 'Dog';    // t || t returns Cat
var o2 = false || 'Cat';    // f || t returns Cat
var o3 = 'Cat' || false;    // t || f returns Cat

// && (논리곱) 연산자
var a1 = 'Cat' && 'Dog';    // t && t returns Dog
var a2 = false && 'Cat';    // f && t returns false
var a3 = 'Cat' && false;    // t && f returns false

// example
function foo (str) {
  str = str || '';
  // do somethig with str
  console.log(str.length);
}

foo();     // 0
foo('hi'); // 2

// example
var obj = {
  // foo: 'hi',
  bar: 'hey'
};

console.log('obj.foo is ' + obj.foo); // obj.foo is undefined

if (obj && obj.foo) {
  // do somethig with obj.foo
  console.log('obj.foo is ' + obj.foo);
}
```



## 6. 타입 연산자 (Type Operators)

| Operator   | Description                              |
| ---------- | ---------------------------------------- |
| typeof     | 피연산자의 데이터 타입(자료형)을 문자열로 반환한다. null과 배열의 경우 object, 함수의 경우 function를 반환하는 것에 유의하여야 한다. |
| instanceof | 객체가 동일 객체형의 인스턴스이면 `true`를 반환한다.         |

```
console.log(typeof 'John');                 // string
console.log(typeof 3.14);                   // number
console.log(typeof NaN);                    // number
console.log(typeof false);                  // boolean
console.log(typeof [1, 2, 3, 4]);           // object
console.log(typeof {name:'John', age:34});  // object
console.log(typeof new Date());             // object
console.log(typeof function () {});         // function
console.log(typeof myCar);                  // undefined (설계적 결함)
console.log(typeof null);                   // object (설계적 결함)

function Person() {}
var me = new Person();
console.log(me instanceof Person); // true
```





## 7. !!

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

