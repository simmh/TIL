# Javascript Introduction



## 1. Javascript는

* 초창기 Javascript는 웹페이지 제작에 있어서 보조적인 기능을 수행하기 위해 한정적인 용도로 주로 사용되었다.
* 웹서버에서 수행되던 많은 역할들이 클라이언트로 이동하였는데 이것은 자바스크립트의 발전 덕분이다. 
* 특히 jQuery의 등장으로 다 DOM(Document Object Model)를 보다 쉽게 제어할 수 있게 되었다.
  ( jQuery는 돔을 직접 조작하였기에 대규모 돔변경시 로직이 변경 되기 때문에 모던웹에선 jquery를 지양한다.)
* C-family languag로 C, Java에서 많은 문법을 차용, Awk, Perl, Python으로부터도 영향을 받음.
* Javascript는  인터프리터 언어(Interpreter language).  compile이 필요없고 HTML파일 안에 직접 기술이 가능.
* Javascript는 멀티-패러다임 언어로 명령형 (imperative), 함수형 (functional), 프로토타입 기반 (prototype-based) 객체지향형 언어다. 

---

## 2. History
JavaScript는 1995년 Brendan Eich(Nescape)이 Navigator 2를 위하여 웹페이지에 포함되는 스크립트 언어로서 개발되었으며 LiveScript로 명명되었다. 이후 Microsoft는 IE 3.0에서 동작하는 JScript를 만들었고 Nescape는 Ecma International에 JavaScript의 표준화를 요청하였다.

* 1997년 7월 ECMA-262라 불리는 명세가 완성. ECMAScript로 명명
* 1999년 ECMAScript 3(ES3)이 공개
* 2009년 출시된 ECMAScript 5(ES5)는 HTML5와 함께 출현한 표준안

---

## 3. ECMAScript Version
* ECMAScript 3 : ECMA-262 3rd edition (1999.12)가장 범용적으로 지원되는 버전이다.
* ECMAScript 5 : ECMA-262 5th edition (2009.12)HTML5와 함께 출현한 표준안이다. JSON(JavaScript Object Notation)과 Strict Mode가 추가되었다. IE 9 이상(85%)이나 그 외 브라우저에서만 작동한다.
* ECMAScript 6 : ECMA-262 6th edition (2015.06)let, const 키워드, Arrow Function, class, Symbol 타입 등이 추가되었다.

---



## 4. 자바스크립트 실행하기

* Javascript는 인터렉티브(interactive)한 웹페이지 작성을 가능하게 한다.
* 정적인 HTML을 동적으로 변경할 수 있는 유일한 방법.
* HTML(구조structure와 내용content 담당)과 Javascript는 역할(관심사 Concern)이 다르므로 분리된 파일로 작성이 바람직



## 5. Browsers Support

* 2017년 1월, IE 제외 대부분 모던 브라우어 ES6 지원하나 97%만 지원. 
* Node.js 경우 v4 부터 지원
* IE 지원 고려한다면 bable과 같은 Transpiler를 사용 해야 한다.

ES6 compat table (https://kangax.github.io/compat-table/es6/)

---


### 5.1. 브라우저 동작 원리

브라우저의 주요 기능은 사용자가 참조하고자 하는 웹페이지를 서버에 요청(Request)하고 응답(Response)을 받아 브라우저에 표시하는 것이다. 
브라우저는 서버로부터 html, css, javascript 파일을 응답받는다. html, css 파일은 렌더링 엔진의 HTML 파서와 CSS 파서에 의해 파싱(Parsing)되어 DOM, CSSOM 트리로 변환되고 렌더 트리로 결합된다.

요소의 가장 아래에 스크립트를 위치시키는 이유

* HTML 요소들이 스크립트 로딩 지연으로 인해 렌더링에 지장 받는 일이 발생하지 않아 페이지 로딩 시간이 단축된다.
* DOM이 완성되지 않은 상태에서 자바스크립트가 DOM을 조작한다면 에러가 발생한다

---

### 5.2Randering Engine
    Paser HTML-> Dom tree (자료 구조 메모리상 저장) ~

Javascript Engine(Webkit)
![Alt text](http://poiemaweb.com/img/client-server.png) 

---



* 디렉터리(Directory)

디렉터리는 파일과 다른 디렉터리를 갖는 파일 시스템 내의 존재물로서 폴더라고도 불리운다.
루트 디렉터리파일 시스템 계층 구조 상의 최상위 디렉터리이다.

```
 Unix: /
 Windows: C:\

# 홈 디렉터리시스템의 사용자에게 각각 할당된 개별 디렉터리이다.
 Unix: /Users/{계정명}
 Windows: C:\Users\{계정명}

# 작업 디렉터리작업 중인 파일의 위치한 디렉터리이다.
  ./

# 부모 디렉터리작업 디렉터리의 부모 디렉토리이다.
 ../
```









# # Reference

[poiemaweb.com/js-introduction](http://poiemaweb.com/js-introduction)