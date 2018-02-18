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
// 배열 중간에 새 배열 추가
var items = ['one', 'four'];
Array.prototype.splice.apply(items, [1, 0].concat(['two', 'three']));
// items.splice(1, 0, ['two', 'three']); 
// [ 'one', [ 'two', 'three' ], 'four' ]
// console.log(items); // [ 'one', 'two', 'three', 'four' ]
// items[1]부터 0개의 요소를 제거하고 그자리(items[1])에 새로운 배열를 추가한다. 제거된 요소가 반환된다.

// items.splice(1, 0, ...['two', 'three']); // ES6
```





### sort(comparefunc)

배열 요소 정렬

```javascript
var fruits = ['Banana', 'Orange', 'Apple', 'Mango'];

fruits.sort(); // ascending(오름차순) ['Apple', 'Banana', 'Mango', 'Orange']
fruits.reverse(); // descending(내림차순) ['Orange', 'Mango', 'Banana', 'Apple']

var points = [40, 100, 1, 5, 25, 10];

points.sort(); // [ 1, 10, 100, 25, 40, 5 ] 1로 시작, 2로 시작?
```





