# 3. Function scope

자바스크립트는 function-level scope

전역 변수와 지역변수가 동일한 이름으로 중복 선언 되었다면, 지역변수 우선 참조

내부 함수는 자신 포함한 외부함수 변수 접근 가능(`실행 컨텍스트`의 스코프 체인에 의해 참조 순위에서 전역변수가 밀림)

함수 내에서 전역변수 참조 가능하면 값도 바꿀수 있다.

내부함수 경우 전역변수, 상위함수 접근/변경 가능

중첩 scope는 가장 인접한 지역을 우선하여 참조한다.

```
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

# 4. 암묵적 전역 (implied globals)

선언 없이 함수내에 할당된 변수는 전역변수로 선언된다.
(혼란의 여지가 있으므로 var keyword는 반드시 사용하자.)

```
function foo() {
  x = 1;   // Throws a ReferenceError in "use strict" mode
  var y = 2;
}

foo();

console.log(x); // 1
console.log(y); // ReferenceError: y is not defined
```



# 5. Lexical scoping (Static scoping)

?????

```
var i = 5;

function foo() {
  var i = 10;
  bar();
}

function bar() { // 선언된 시점에서의 scope를 갖는다!
  console.log(i);
}

foo(); // ?
```

