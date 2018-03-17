# 9.1 Node.js Basics

네트워크 애플리케이션을 위한 자바스크립트 런타임 환경

```
note. 프론트엔트
상태변화 -> DOM, Event, Ajax
```

## 1 Introduction

* Node.js는 Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임 환경(Runtime Environment)
* 서버 사이드 애플리케이션 개발에 사용되는 소프트웨어 플랫
* 2009년 [Ryan Dahl](https://en.wikipedia.org/wiki/Ryan_Dahl)이 발표된 Node.js
* Node.js는 **Non-blocking I/O와 단일 스레드 이벤트 루프**를 통한 높은 Request 처리 성능을 가지고 있다.



## 2 install

```
http://nodejs.org/

update
$ npm install -g n

캐시 강제 삭제
$ npm cache clean -f
```





## 5 Node.js 맛보기: HTTP Server

```javascript
// app.js
const http = require('http'); // 1

http.createServer((request, response) => { // 2
  response.statusCode = 200;
  response.setHeader('Content-Type', 'text/plain');
  response.end('Hello World');
}).listen(3000); // 3

console.log('Server running at http://127.0.0.1:3000/');
```

1. http 모듈을 로딩하여 변수 http에 할당하였다.
   (http 내장 모듈)
2. http 모듈의 `createServer([requestListener])` 메소드를 사용하여 HTTP 서버 객체를 생성한다. HTTP 서버 객체는 [EventEmitter](https://nodejs.org/dist/latest-v8.x/docs/api/events.html#events_class_eventemitter) 클래스를 상속한 것으로 request 이벤트가 발생하면 HTTP request를 처리하여 response를 반환하는 request Listener 함수를 호출한다. 이 request Listener 함수는 request와 response 객체를 전달받으며 HTTP request 이벤트가 발생할 때마다 한번씩 호출된다.
3. createServer 메소드가 반환한 HTTP 서버 객체의 listen 메소드에 포트번호 3000를 전달하여 서버를 기동시킨다.



실행

```
> node app.js //서버실행 
> npm i -g nodemon //와치모드 앱 설치

```



# *9.2* Node.js & **npm**

## 모듈화와 npm(node package manager)

## 1 모듈화와 CommonJS



```
> npm install  package.json// 일괄 환경
> npm install <package> // 패키지 설치
```





## package.json 의존성(dependency) 관리

1 

패키지를 설치할 때 package.json을 찾을 수 없다는 경고가 발생

```
npm init
npm init -y //default 설정
```



2. 패키지 설치

```
npm install <package>
```



3 

```
$ npm init -y
Wrote to /Users/leeungmo/Desktop/emoji/package.json:

// 폴더명과 패키지명 같으면 error
{
  "name": "emoji", 
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": { // 기본 npm install 서버에도 배포
    "node-emoji": "^1.8.1" // 
  },
  "devDependencies": {}, // 개발용 --save -dev
  "scripts": { //실행할 쉘스크립트
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```



2.4 Semantic versioning(유의적 버전)

```
$ npm install node-emoji@1.5.0 // @버전
...
  "dependencies": {
    "node-emoji": "^1.5.1"
  },
...
```



패키지 지정 설치 

npm install  {{패키지명}}@{{버전}} 

버전 범위 지정없이 기록. 다시설치시 최신버전

--save-exact

메이저 버전 번호, 마이너 버전 번호, 패치 버전 번호

1.7.3



# *9.3* Node.js **module**

## Node.js의 module loading system

## 1 Node.js 모듈

## 2 exports

모듈은 독립적인 파일 스코프를 갖는다.
해당 모듈 내부에서만 참조 가능하다.
모듈 안에 선언한 항목을 외부 공개-> exports 객체 사용

모듈을 파일로 작성
외부공개 대상 exports 객체의 프로퍼티or 메소드 정의
모듈을 전역 함수 require()이용하여 추출

<module JS 파일>

```javascript
// circle.js 독립적인 파일 스코프를 갖는 모듈
const { PI } = Math; // private 변수
exports.area = (r) => PI * r * r;
exports.circumference = (r) => 2 * PI * r;
// area, circumference를 exports 객체의 메소드로 정의
```

<모듈 사용하는 JS 파일>

```javascript
// app.js
const circle = require('./circle.js'); // == require('./circle')

console.log(`지름이 4인 원의 면적: ${circle.area(4)}`);
console.log(`지름이 4인 원의 둘레: ${circle.circumference(4)}`);
```

< 실행 결과>

```
$ node app
지름이 4인 원의 면적: 50.26548245743669
지름이 4인 원의 둘레: 25.132741228718345
```



## 3 module.exports

|      구분      | 모듈 정의 방식                                               | require 함수의 호출 결과                                     |
| :------------: | :----------------------------------------------------------- | :----------------------------------------------------------- |
|    exports     | **exports 객체에는 값을 할당할 수 없음 <br />공개할 대상을 exports 객체에<br />프로퍼티 또는 메소드로 추가.** | exports 객체에 추가한 프로퍼티와 메소드가 담긴 객체가 전달 됨 |
| module.exports | **module.exports 객체에 <br />하나의 값(기본자료형, 함수, 객체)만을 할당.** | module.exports 객체에 할당한 값이 전달 됨.                   |



> exports는 module.exports에의 참조, 
> module.exports의 alias. 
> exports ==  module.exports 같다고 봐도 무방
>
> 어렵게 느껴진다면 exports를 무시하고 module.exports만을 사용하라고 권유하고 있다.



## 3.1 module.exports에 함수를 할당하는 방식

```javascript
// foo.js
module.exports = function(a, b) { 
  return a + b;
};
```

```javascript
// app.js
const add = require('./foo');

const result = add(1, 2);
console.log(result); // => 3
```



## 3.2 exports에 객체를 할당하는 방식

```javascript
// foo.js
// 객체를 사용하여 복수의 기능을 하나로 묶어 공개하는 방식
module.exports = {
  add (v1, v2) { return v1 + v2 },
  minus (v1, v2) { return v1 - v2 }
};
```

```javascript
// app.js
const calc = require('./foo');

const result1 = calc.add(1, 2);
console.log(result1); // => 3
```



# 4. require

```javascript
// 모듈 명시하지 않고 require 함수를 호출하면 해당 폴더 index.js 로드
const myModule = require('./module'); //
```

----

```javascript
// module/index.js
module.exports = {
  calc: require('./calc'),
  print: require('./print')
};
```

```javascript
// app.js
const myModule = require('./module');

// module/calc.js의 기능
const result = myModule.calc.add(1, 2);

// module/print.js의 기능
myModule.print.sayHello();
```



# 5. 코어 모듈과 파일 모듈

코어모듈(Node.js) , 외부 패키지 패스 명시 않아도 무방

그외 모든 파일 모듈 로딩시 패스 명시.

```
const http = require('http'); // 코어 or 패기지 모듈
const foo = require('./lib/foo'); // 파일
```



# Reference

http://poiemaweb.com/nodejs-module