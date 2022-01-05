# 개요
- 주로 [TOAST UI-HTML/CSS/Sass](https://ui.toast.com/fe-guide/ko_HTMLCSS), [TOAST UI-코딩컨벤션](https://ui.toast.com/fe-guide/ko_CODING-CONVENTION)을 참고
- 주요 내용 중 개인적으로 헷갈리는 내용이나 수정한 개인의 컨벤션 규칙을 정리하기 위해 작성한 문서

# 목록
- [HTML](#HTML)
- [CSS](#CSS)
- [SCSS](#SCSS)
- [JS](#JS)

# <span id="HTML">HTML</span>

## Boolean 속성은 값을 따로 명시하지 않는다.
selected, disabled, checked 등의 Boolean 속성은 값을 따로 명시하지 않는다.

```html
<!-- Bad -->
<input type="text" disabled=true>

<!-- Good -->
<input type="text" disabled>

<!-- Good -->
<input type="checkbox" value="1" checked>

<!-- Bad -->
<input type="checkbox" value="1" checked=true>

<!-- Good -->
<select>
  <option value="1" selected>1</option>
</select>

<!-- Bad -->
<select>
  <option value="1" selected=true>1</option>
</select>
```

## 불필요한 태그 작성은 피한다.
자세한 내용은 [[FE 가이드] 성능 가이드 문서](https://ui.toast.com/fe-guide/ko_PERFORMANCE)
```html
<!-- Bad -->
<span class="tui">
  <img src="...">
</span>

<!-- Good -->
<img class="tui" src="...">
```

## 엔티티 참조는 사용하지 않는다.
다만 HTML에서 의미가 있는 `<`나 `&` 등 문자는 엔티티 참조를 사용해야 한다.
```html
<!-- Bad -->
The currency symbol for the Euro is `“&eur;”`.

<!-- Good -->
The currency symbol for the Euro is “€”.
```

# <span id="CSS">CSS</span>

## 기본 스타일
```css
/*
  들여쓰기 공백 2문자
  케밥-케이스
  시작하는 {앞에는 공백 1개 닫는 }는 개행하여 작성
  속성: 값; 형태로 선언 후 공백 1개
  단일 스타일은 한 줄에, 다중 선택시 한 줄씩
  모든 값 뒤에는 ;
*/

.selector {padding:15px;}
.selector {
  padding: 15px;
  margin: 15px;
}
.selector,
.selector-secondary {
  ...
}
```

## 자바스크립트 Hook에서 스타일 지정을 위해 만들어진 클래스를 사용하지 않는다.
- 스타일과 동작 제어의 분리 관리를 위해 스타일을 위한 클래스는 js에서 사용하지 않는다.
- js를 위한 클래스의 경우 `js-{클래스}` 식으로 접두어 방식을 권장한다.
```html
<button class="btn js-submit">submit</button>
```

## 숫자 0 값 이후에는 불필요한 단위를 작성하지 않는다.
```css
/* 0은 0 */
/* Good */
div {
  padding: 0;
  flex: 0px; // flex-basis 컴포넌트의 경우 단위가 필요함
}

/* border가 없을 경우 none대신 0을 사용한다. */
/* Bad */
.no-border {border: none;}

/* Good */
.no-border {border: 0;}
```

## 태그 선택자 대신 클래스 선택자를 사용한다.
- 렌더링 성능을 위해 가능한 한 태그 선택자보다 클래스 선택자를 사용한다.
- 부모 선택자는 반드시 필요한 경우에만 사용한다.
```css
/* Bad */
.page-container #stream .stream-item .tweet .tweet-header .username { ... }

/* Good */
.tweet-header .username { ... }
```

## 가능한 한 축약형을 사용한다.
불필요하게 축약형을 과용하는 것은 피한다.
```css
/* Bad */
.element {
  margin: 0 0 10px 0;
  background: #c83636;
  background: url("back.jpg");
}

/* Good */
.element {
  margin-bottom: 10px;
  background-color: #c83636;
  background-image: url("back.jpg");
}
```

# <span id="SCSS">SCSS</span>

## .scss 문법을 사용한다.
들여쓰기 기반 .sass문법 대신 CSS에서 사용하는 모든 문법과 기능이 완전히 호환되도록 만든 .scss 문법을 사용하도록 한다.
```scss
/* .sass 문법 */
.black-div
  background: black
  border: 1px solid #ccc
  span 
    padding: 10px;

/* .scss 문법 */
.black-div {
  background: black;
  border: 1px solid #ccc;
  span {
    padding: 10px;
  }
}
```

## 선언 순서
속성, @include, 중첩 선택자 순으로 선언한다. @include 선언 이후에는 개행을 한다.
```scss
.black-div {
  background: black;
  border: 1px solid #ccc;
  @include transition(background 0.5s ease)
    
  .icon {
    padding: 10px;
  }
}
```

## mixin
믹스인은 중복되는 스타일을 분리하거나 복잡한 스타일을 추상화하는 역할 등을 위해 마치 함수처럼 사용해야 한다. 특히 인자가 없는 믹스인은, Gzip과 같은 압축 과정 없이는 불필요한 중복 코드를 만들어낼 수 있으므로 주의한다.

## Extend 지시자는 사용하지 않는다.
@extend는 직관적이지 않고 중첩 선택자와 함께 사용하게 될 때 문제가 발생할 수 있기 때문에 사용하지 않는다. Gzip과 믹스인을 사용하면 @extend 지시자 장점을 충분히 얻을 수 있다.

## 선택자 중첩은 최대 3단계까지만 사용한다.
3단계를 넘으면 HTML과 너무 밀접하게 엮여있거나 재사용할 수 없는 CSS를 작성하고 있을 가능성이 크다.

# <span id="전채">전채</span>

## 명명 규칙
- 상수는 영문 대문자 스네이크 표기법(Snake case)를 사용.
- 생성자는 대문자 카멜 케이스을 사용한다.
- 변수, 함수에는 카멜 케이스을 사용한다.
- (지역 변수 or private 변수)명은 '_'로 시작한다.
```js
SYMBOLIC_CONSTANTS;   // 상수는 영문 대문자 스네이크 표기법(Snake case)를 사용.

class ConstructorName { // 생성자는 대문자 카멜 케이스을 사용한다.
  ...
};

let variableName; // 변수, 함수에는 카멜 케이스을 사용한다.
const dogs = [];  // 배열 - 배열은 복수형 이름을 사용
const rDesc = /.*/; // 정규표현식 - 정규표현식은 'r'로 시작

function getPropertyName() {  // 함수
  ...
}

// 이벤트 핸들러 - 이벤트 핸들러는 'on'으로 시작
const onClick = () => {};
const onKeyDown = () => {};

let isAvailable = false;  // 불린 반환 함수 - 반환 값이 불린인 함수는 'is'로 시작
let _privateVariableName; // (지역 변수 or private 변수)명은 '_'로 시작한다.
```

## 선언과 할당
### 변수
- const : 값이 변하지 않는 변수
- let : 값이 변하는 변수
- var : 절대 사용 X
- const를 let 보다 위에 선언한다.
- const와 let은 사용 시점에 선언 및 할당을 한다. (블록 스코프이므로 호이스팅되지 않는다)
- var 선언과 할당의 분리를 허용하는 경우 선언만 하는 변수는 var을 한 번만 사용하는 방식을 허용한다. 
- var 사용 시 블록 스코프 안에서 변수를 선언하지 않는다.

```js
// Bad - var를 한 번만 사용하여 선언
var foo = '',
  bar = '',
  quux = '';

// Good - 변수 별 var 선언
var foo = '';
var bar = '';
var quux = '';

// Good - 선언과 할당의 분리인 경우 한 줄로 연결 허용
var foo, bar, quux;


// Bad
var length = 100;
for (var i = 0; i < length; i += 1) {
  ...
}

// Good
var i = 0;
var length = 100;
for (; i < length; i += 1) {
  ...
}
```
### 배열과 객체
배열과 객체는 반드시 리터럴로 선언한다.
배열 복사 시 순환문을 사용하지 않고 전개 연산자를 사용한다.
```js
// Bad
const emptyArr = new Array();
const arr = new Array(1, 2, 3, 4, 5);

// Good
const emptyArr = [];
const arr = [1, 2, 3, 4, 5];


const len = items.length;
let i;

// Bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// Good
const itemsCopy = [...items];
```

객체의 메서드 표현 시 축약 메소드 표기를 사용한다.
메서드 문법 사용 시 메서드 사이에 개행을 추가한다.

```js
// Bad
const atom = {
  value: 1,

  addValue: function(value) {
    return atom.value + value;
  }
};

// Good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  }
};

// Good
class MyClass {
  foo() {
    //...
  }
      // 이렇게 공백
  bar() {
    //...
  }
}

```
... 이 사이는 JS 작업 이후에 다시보기 ...

## 블록 구문
- 한 줄 짜리여도 {}를 생략하지 않는 것이 좋다.
- 키워드와 조건문 사이에 빈칸을 사용한다.
- do-while문 사용 시 while문 끝에 세미콜론을 쓴다.
- switch-case 사용 시 첫 번째 case문을 제외하고 case문 사용 이전에 개행한다.
- switch-case 사용 시 각 구문은 break, return, throw 중 한 개로 끝나야 하며 default문이 없으면 // no default 표시를 해준다.
