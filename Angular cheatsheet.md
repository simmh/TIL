# Angular CLI

 Angular CLI  <https://cli.angular.io/>





# 컴포넌트 

![change detection](http://poiemaweb.com/img/change-detection.png)



```typescript
    sayHi() {
    return `Hi! my name is ${ this.name }.`;
    }
}
```



## 1 데이터 바인딩

| 데이터 바인딩 | 문법                               |
| ------------- | ---------------------------------- |
| 인터폴레이션  | {{ expression }}                   |
| 프로퍼티      | [property]=”expression”            |
| 어트리뷰트    | [attr.attribute-name]=”expression” |
| 클래스        | [class.class-name]=”expression”    |
| 스타일        | [style.style-name]=”expression”    |
| 이벤트        | (event)=”statement”                |
| 양방향 데이터 | [(ngModel)]=”variable”             |



### 인터폴 레이션

```html
<p>sayHi(): {{ sayHi() }}</p>
<p>age * 10: {{ age * 10 }}</p>
<p>age > 10: {{ age > 10 }}</p>

<p>{{ contents }}</p> == <p [innerHTML]="contents"></p>
<input type="text" value="{{ name }}">
```



### 프로퍼티 바인딩

```html
<element [property]="expression">...</element>

<input type="text" [value]="name"> <!-- value 컴파일시 없어짐 -->
<p [innerHTML]="contents"></p>
<img [src]="imageUrl">
<button [disabled]="isDisabled">disabled button</button> //isDisabled = true;
```



#### value 와 attr.value

```
<!-- 프로퍼티 바인딩 -->
<input id="user" type="text" [value]="name">
<!-- 어트리뷰트 바인딩 -->
<input id="user" type="text" [attr.value]="name">
```





### 어트리뷰트 바인딩

```html
<element [attr.attribute-name]="expression">...</element>

<input id="user" type="text" [attr.value]="name"> <!--초기값 -->

<!-- colspan 프로퍼티는 존재하지 않기 때문에 어튜리뷰트 바인딩을 사용한다. -->
<td [attr.colspan]="length">A + B</td>
```



### 클래스 바인딩

```html
<element [class.class-name]="booleanExpression">...</element>
<element [class]="class-name-list">...</element>
<!--여러개 지정시 ngClass 디렉티브를 사용 -->
```

```html
<!-- 조건의 의한 클래스 바인딩
우변의 표현식이 true이면 클래스를 추가한다 -->
<div [class.text-large]="isLarge">text-large</div>

<!-- 조건의 의한 클래스 바인딩
우변의 표현식이 false이면 클래스를 삭제한다 -->
<div class="text-small color-red" [class.color-red]="isRed">text-small</div
>

<!-- 여러 클래스 한번에 지정 -->
<div [class]="myClasses">text-large color-red</div>

<!-- 클래스 바인딩은 기존 클래스 어트리뷰트보다 우선한다.
기존 클래스 어트리뷰트는 reset된다. 위치는 관계X -->
<div class="text-small color-blue" [class]="myClasses">text-large color-red
</div>
```





### 스타일 바인딩 

```html
<element [style.style-property]="expression">...</element>
```

```html
이벤트 바인딩은 구문이라 할당 가능. 
<button class="btn" 
	[style.background-color]="isActive ? '#4CAF50' : '#f44336'"
	[style.font-size.em]="isActive ? 1.2 : 1" 
     (click)="isActive=!isActive">Toggle
</button>
```



### 이벤트 바인딩

```html
<element (event)="statement">...</element>
```

```typescript
@Component({
selector: 'app-root',
template: `
    <input type="text" [value]="name" (input)="onInput($event)">
    <button (click)="onClick()">clear</button>
    <p>name: {{ name }}</p>
    `
})
export class AppComponent {
    name = '';
        onInput(event) {
        console.log(event);
    // event.target.value에는 사용자 입력 텍스트가 담겨있다.
    this.name = event.target.value;
    }
    onClick() {
    	this.name = '';
    }
}
```



### 양방향 데이터 바인딩

#### (프로퍼티 + 이벤트 바인딩)

```html
<element [(ngModel)]="property">...</element>
```

* src/app/app.module.ts에 모듈 추가 필수 !

  import { FormsModule } from '@angular/forms';

```html
<!-- 동일 동작 -->
<!--양방향 바인딩 -->
<input type="text" [(ngModel)]="name">
    <p>name: {{ name }}</p>

<!--프로퍼티 + 이벤트 바인딩 -->
<input type="text" [value]="name" (input)="name=$event.target.value">
    <p>name: {{ name }}</p>
```





## 2 빌트인 디렉티브

### 빌트인 어트리뷰트 디렉티브

### ngClass



### ngStyle



## 3 빌트인 구조 디렉티브

### ngIf

```html
<element *ngIf="expression">...</element>
<!-- 위와 같음 -->
<ng-template [ngIf]="expression">
  <element>...</element>
</ng-template>
```

예제. 1

```html
<!-- ngIf에 의한 show/hide -->
<p *ngIf="isShow">Lorem ipsum dolor sit amet</p>

<!-- 스타일 바인딩에 의한 show/hide -->
<p [style.display]="isShow ? 'block' : 'none'">Lorem ipsum dolor sit amet</p>

<button (click)="isShow=!isShow">{{ isShow ? 'Hide' : 'Show' }}</button>
```

예제. 2

```html
<style>
	.text-small { font-size: 18px;}
    .text-large { font-size: 36px;}
    .color-blue { color: blue;}
    .color-red { color: red;}
</style>

<!-- true면 추가 -->
<div [class.text-large]="isLarge">text-large</div>

<!-- false면 삭제 --> 
<div class="text-small color-red" [class.color-red]="isRed">text-small</div>

<!-- 클래스 여러개 지정, 기존클래스 reset, 위치 상관 X -->
myClasses = 'text-large color-red';
<div [class]="myClasses">text-large color-red</div>

<div class="text-small color-blue" [class]="myClasses">text-large color-red</div>


export class AppComponent {
  isLarge = true;
  isRed = false;
  // 클래스 바인딩은 문자열을 바인딩한다.
  myClasses = 'text-large color-red';
}
```







### ngFor

first, last, even, odd

리스트가 많을 시 속도 이슈. trackBy 사용 (비추)

```html
<element *ngFor="let item of items">...</element>
<element *ngFor="let item of items; let i=index; let odd=odd; trackBy: trackById">...</element>

<!-- 위와 같음 syntactic sugar-->
<ng-template ngFor let-item [ngForOf]="items">
  <element>...</element>
</ng-template>

<ng-template ngFor let-item [ngForOf]="items" let-i="index" let-odd="odd" [ngForTrackBy]="trackById">
  <element>...</element>
</ng-template>
```

예제.

```html
<!-- user를 추가한다 -->
<input type="text" #name placeholder="이름을 입력하세요">
<button (click)="addUser(name.value)">add user</button>
<ul>
  <!-- users 배열의 length만큼 반복하며 li 요소와 하위 요소를 DOM에 추가한다 -->
  <li *ngFor="let user of users; let i=index">
    {{ i }}: {{ user.name }}
    <!-- 해당 user를 제거한다 -->
    <button (click)="removeUser(user.id)">X</button>
  </li>
</ul>
<pre>{{ users | json }}</pre>
```



### ngSwitch

```html
<element [ngSwitch]="expression">
  <!-- switch 조건이 'case1'인 경우 DOM에 추가 -->
  <element *ngSwitchCase="'case1'">...<element>
  <!-- switch 조건이 'case2'인 경우 DOM에 추가 -->
  <element *ngSwitchCase="'case2'">...<element>
  <!-- switch 조건과 일치하는 ngSwitchCase가 없는 경우 DOM에 추가 -->
  <element *ngSwitchDefault>...<element>
</element>
```

원래 구문

```html
<element [ngSwitch]="expression">
  <ng-template [ngSwitchCase]="'case1'">
    <element>...</element>
  </ng-template>
  <ng-template [ngSwitchCase]="'case2'">
    <element>...</element>
  </ng-template>
  <ng-template ngSwitchDefault>
    <element>...</element>
  </ng-template>
</element>
```

예제

```html
<input type="text" [(ngModel)]="num" placeholder="숫자를 입력하세요">
    <div [ngSwitch]="num">
      <div *ngSwitchCase="'1'">One</div>
      <div *ngSwitchCase="'2'">Two</div>
      <div *ngSwitchCase="'3'">Three</div>
      <div *ngSwitchDefault>This is Default</div>
    </div>
```







## 4 Template reference

 variable & Safe navigation operator



### [ # ] 템플릿 참조 변수(Template reference variable) 

* DOM 요소에 대한 참조를 담고 있는 변수
* 템플릿 내에서만 유효하며 컴포넌트
* 템플릿 참조 변수의 값을 이벤트 바인딩을 통해 컴포넌트 클래스로 전달할 수는 있다

```
<element #myelement>...</element>
```

예제.

```html
<div>
<!-- 템플릿 참조 변수 email의 선언 -->
<input #email type='email' placeholder="이메일을 입력하세요">
<!-- 템플릿 참조 변수 email의 참조 -->
<button (click)="checkEmail(email.value)">이메일 형식 체크</button>
</div>
<span *ngIf="result">{{ result }}</span>
```



###  [ ? ] 세이프 내비게이션 연산자

```html
<!-- obj가 null 또는 undefined일 때 공백 -->
{{ obj }}

<!-- obj가 프로퍼티 null 또는 undefined일 때 erro 
ERROR TypeError: Cannot read property 'id' of undefined -->
{{ obj.id }}

<!-- safe 연산자: 프로퍼티 null 또는 undefined일때 나는 erro를 pass 처리 -->
{{ obj?.id }}
```





## 5 Interaction

http://poiemaweb.com/angular-component-interaction

### 부모 - 자식 컴포넌트 연결

app.component.ts(부모) 와 user-list.component.ts (자식) 연결

app/

​	ueser-list/

```typescript
app.compenet.ts (부모)
@Componet ({
    selector: 'app-root',
    template: `
        <!-- 자식 컴포넌트 추가 -->
        <app-user-list></app-user-list>
    `
    styles: []
})
```



#### 모델 클래스 추가

일관성 유지 인터페이스

```bash
$ ng g cl models/user.model
```

User 모델 클래스 추가

```typescript
// models/user.model.ts
export class User {
    constructor(public id: number, public name: string, public role: string) { }
}
```



#### 부모 → 자식 [데이타 바인딩] 

Property binding [`state`: myState]

부모: < child [`state`] ="myState">< /child>

자식: @Input() `state`:string;

```typescript
// app.component.ts

import { User } from '../models/user.model'

// template:
`<app-user-list [users]="users"></app-user-list>`

//note. bad. 실습때 기본 데이터 지정용
// export class AppComponent { constructor(): }
constructor() {
    this.users = [
        new User(1, 'Lee', 'Administrator'),
        new User(2, 'Baek', 'Developer'),
        new User(3, 'Park', 'Designer')
        ];
}
```



#### 자식 컴포넌트(user-list.component.ts)

@Input 데코레이터를 통 해 컴포넌트 프로퍼티 users에 바인딩

```typescript
// user-list.component.ts
//import input , User
import { Component, Input } from '@angular/core';
import { User } from '../models/user.model'
...
export class UserListComponent {
@Input() users: User[];
}

```



### 자식 → 부모 [data binding]



## 6 CSS framework 적용

uikit 설치

```
npm i uikit // 확인필요
```

* `.angular-cli.json` 수정


* js 추가시 순서중요 
* 서버 재시작

```typescript
"styles":[
	"../node_modules/uikit/dist/css/uikit.min.css",
     "styles.css"
 ],
"scripts": [
     "../node_modules/uikit/dist/js/uikit.min.js",
     "../node_modules/uikit/dist/js/uikit-icons.min.js"        
      ],
 
* js 추가시 순서중요 
* 서버 재시작
```

