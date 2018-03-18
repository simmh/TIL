# Array

## 

### 타입

```javascript
var arr = [1,2,..]
console.log(typeof arr);  // object
console.log(Array.isArray(arr)); //true
```

### 생성

```javascript
var arr = new Array(2);  // 2 [undefined, undefined] // [empty × 2]
var arr = new Array(1, 2, 3); //  [1, 2, 3]

var arr = [];
arr[0] = 'one';
arr[1] = undefined;
arr[7] = 'seven'; //  ["one", undefined × 2, "three", undefined × 3, "seven"]

```

### 삭제

```javascript
delete arr[2]; // 해당 index = undefined
arr.splice(2, 1); // 시작 인덱스, 삭제할 요소 갯수
```

### 배열 요소 열거

```javascript
//for in 문은 불필요한 프로퍼티까지 출력, 순서 보장 x
// 그냥 for 문 사용.

for (var i = 0; i < numbersArr.length; i++) {
  console.log(i, numbersArr[i]);
  // 0 'zero' / 1 'one' / 2 'two' / 3 'three'
}

```







## Array Property



### Array.isArray()

```javascript
// true
Array.isArray([]); //빈요소 true
Array.isArray([1, 2]);
Array.isArray(new Array());

// false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(1);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
```



### concat() 배열 연결

배열 or 값 연결 , `복사본` 반환 , `원본 수정 x` 

```javascript
var c = a.concat(b); 
var d = a.concat('String'); // ['a', 'b', 'c', 'String']
var e = a.concat(b, true); // ['a', 'b', 'c', 'x', 'y', 'z', true]
```



### join() 요소 연결

배열 요소 전체 연결, `복사본` 반환 , `원본 수정 X` 
+연산자보다 빠름

```javascript
str = arr.join([separator = ','])  

var x = arr.join(); // 'a,b,c,d';
var y = arr.join('');  // 'abcd'
```



### reverse()

배열요소 순서 반대로 변경, `변경된 배열`반환,  `원본 수정 o`

```javascript
var b = a.reverse();
console.log(a); // [ 'c', 'b', 'a' ] 변경된 원본
console.log(b); // [ 'c', 'b', 'a' ] 변경된 원본의 복사본
```



### push() 마지막에 추가

인자 배열 끝에 추가, `배열 길이` 반환, `원본 수정 O`, `performance 별로 `

```javascript
var c = a.push(b);
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];
var c = a.push(b); // a --> ['a', 'b', 'c', ['x', 'y', 'z']]
console.log(c); // c --> 4; 배열 길이 (legnth)반환
```



### pop() 마지막 제거 

마지막 요소제거, `제거된 요소 `반환, `원본 수정 O`

```javascript
var c = a.pop();
console.log(c); // c --> 'c' 제거된 요소
```



### shift() 첫 제거

첫요소 제거, `제거된 요소` 반환, `원본 수정 O`
push() 와 함께 큐 (FIFO) 처럼 동작 가능, 빈 배열일 경우 `undefined`를 반환 ?

```javascript
var a = ['a', 'b', 'c'];  
var c = a.shift(); // a --> [ 'b', 'c' ] // c --> 'a'
```

unshift?

### slice() 배열요소 복사

slice(start, [end:기본값 length])

배열 특정 부분 복사,  `복사본` 반환 ,  `원본 수정 X` 

```javascript
var items = ['a', 'b', 'c']; // [0:'a', 1:'b', 2:'c']

var res0 = items.slice(0) //['a', 'b', 'c'] [0]부터 모든 요소
var res1 = items.slice(0, 1); // [ 'a' ] [0] ~ [1]이전까지 == [0]
var res2 = items.slice(1, 2); // [ 'b' ] [1] ~ [2]이전까지 == [1]
var res4 = items.slice(-2); // [ 'b', 'c' ] 끝에서 2개

var res5 = items.slice(); // res5 = items 모든 요소 반환 본사본 생성
```

#### snippet

```javascript
var copy = origin.slice(); // 배열복사
```



### splice() 배열 요소 제거

기존 배열 요소 제거 + 새 요소 추가, `삭제한 요소들 배열` 반환, `원본 수정O`

splice(시작 인덱스, 제거할 갯수, [삭제 위치에 추가 요소])

```javascript
// 주로 배열 요소 삭제에 사용.
var items = ['one', 'two', 'three', 'four']; // -> [ 'one', 'four' ]
var res = items.splice(1, 2); [1]부터 2개 제거
console.log(res);   // [ 'two', 'three' ] 제거 요소 배열 반환
```
```javascript
//삭제 후 요소 추가
var res = items.splice(1, 2, 'x', 'y'); //[1]부터 2개 제거, 'x','y' 추가
console.log(res);   // [ 'two', 'three' ] 제거 요소 배열 반환
```

```javascript
//기존 배열에 요소 추가
var items = ['one', 'two', 'three', 'four']; 
var res = items.splice(1, 0,x); [1]뒤에 x 추가?
```



```javascript
// 배열 중간에 새 배열 추가
var items = ['one', 'four'];
Array.prototype.splice.apply(items, [1, 0].concat(['two', 'three']));
// items.splice(1, 0, ['two', 'three']); 
// [ 'one', [ 'two', 'three' ], 'four' ]
// console.log(items); // [ 'one', 'two', 'three', 'four' ]
// items[1]부터 0개의 요소를 제거하고 그자리(items[1])에 새로운 배열를 추가한다. 제거된 요소가 반환된다.

// items.splice(1, 0, ...['two', 'three']); // ES6
```

splice를 호출하고 싶다. 대상이 배열이다.
apply 2번째 인자는 매개변수 리스트.

str === str.split('').reverse().join('');



### sort(comparefunc)

배열 요소 정렬

```javascript
var fruits = ['Banana', 'Orange', 'Apple', 'Mango'];

fruits.sort(); // ascending(오름차순) ['Apple', 'Banana', 'Mango', 'Orange']
fruits.reverse(); // descending(내림차순) ['Orange', 'Mango', 'Banana', 'Apple']

var points = [40, 100, 1, 5, 25, 10];

points.sort(); // [ 1, 10, 100, 25, 40, 5 ] 1로 시작, 2로 시작?
```



```javascript
// 숫자 배열 -- 암기 영역
// 숫자 배열 오름차순 정렬
// compareFunction의 반환값이 0보다 작은 경우, a를 우선한다.
points.sort(function (a, b) { return a - b; });
console.log(points); // [ 1, 5, 10, 25, 40, 100 ]

// 숫자 배열 내림차순 정렬
// compareFunction의 반환값이 0보다 큰 경우, b를 우선한다.
points.sort(function (a, b) { return b - a; });
console.log(points); // [ 100, 40, 25, 10, 5, 1 ]

console.log(points[0]); // 1
```



### forEach() 

배열 각 요소에 함수(로직)처리,  `함수 통과값 처리된 배열` 반환 ,  `원본 수정 시킬수도  ` 

고차함수, break 못씀 syntexterro. for보다 성능 않좋음, IE9 이상

```javascript
var total = 0;
var testArray = [1, 3, 5, 7, 9];


// 원본 배열을 변경하려면 콜백 함수의 3번째 인자를 사용한다.
testArray.forEach(function (item, index, array) { //array=this
  array[index] = Math.pow(item, 2);  //전역 함수 부분
});
// [1, 2, 3].forEach
```



### map()

요소마다 함수처리, `결과값들의 새 배열` 반환,  `원본 수정x ` 

원본 배열수 만큼 처리된 배열 반환. 꼭 return 

```javascript
var numbers = [1, 4, 9];
var roots = numbers.map(function (item) { // 요소마다 제곱근 뽑기
  return Math.sqrt(item);  //return 없으면 빈배열[]
var roots = numbers.map(Math.sqrt); // 위에꺼 축약
```





### filter()

순회, `true 통과한 요소값 새배열` 반환,  `원본 수정x ` 

```javascript
var result = [1, 2, 3, 4, 5].filter(function (item, index, array) {
  console.log('[' + index + '] = ' + item);
  return item % 2; // 홀수만을 필터링한다 (1은 true로 평가된다) //조건식
}); // [1,3,4]
```



### reduce()

```javascript
//previousValue 에 순회한 요소 계속 더하는 예제
var result = [1, 2, 3, 4, 5].reduce(function (previousValue, currentValue, currentIndex, array) {
  console.log(previousValue + '+' + currentValue + '=' + (previousValue + currentValue));
  return previousValue + currentValue; // 결과는 다음 콜백의 첫번째 인자로 전달된다
});


```



### some()

콜백함수의 테스트를 통과하는지 확인, boolean으로 반환



### every() 모두 통과?

모든 요소가 콜백함수의 테스트를 통과하는지, boolean으로 반환



### find() 참인 첫 요소

ES6, IE 안됨

```javascript
// 콜백함수를 실행하여 그 결과가 참인 첫번째 요소를 반환한다.
var result = array.find(function (item) {
  return item.id === 2;
});

// filter는 콜백함수의 실행 결과가 true인 배열 요소의 값만을 추출한 새로운 배열을 반환한다.
result = array.filter(function (item) {
  return item.id === 2;
});
```







### mozilla array 

[mozilla array]: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array

