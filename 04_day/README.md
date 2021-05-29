# 4일차

## CSS

### CSS Reset

> 브라우저별 설정된 기본 style이 다르므로 이를 통일시키기 위해 초기화 시킨다.

- [reset.css cdn](https://www.jsdelivr.com/package/npm/reset-css)

### Emmet

> 선택자를 통해 쉽게 태그를 만드는 문법

## CSS 개요, 선택자, 상속

### 기본 문법

- 선택자

  ```css
  선택자 {
    속성: 속성값;
    속성: 속성값;
  }

  div {
    background: red;
  }
  ```

- 주석

  ```css
  /*Comment*/
  ```

### 선언방식

- 인라인(in-line) 방식 : HTML 요소(태그)의 `'style'` 속성에 직접 작성

  ```html
  <div style="color:red;">in-line css</div>
  ```

  - 직접 손으로 입력하는 행위는 지양(유지보수가 힘듦)

- 내장(embedded) 방식 : HTML `<style></style>` 안에 작성하는 방식

  ```html
  <head>
    <style>
      div {
        color: red;
      }
    </style>
  </head>
  <body>
    <div>embedded</div>
  </body>
  ```

- 링크(link) 방식 : HTML `<link>`를 이용하여 외부 CSS 문서를 불러와 적용하는 방식

  ```html
  <head>
    <link rel="stylesheet" href="./main.css" />
  </head>
  <body>
    <div>link</div>
  </body>
  ```

  - 병렬 호출, 거의 동시에 불러오기가 완료

- @import(at import) 방식 : CSS의 @import를 이용하여 외부 CSS 문서를 불러와 적용하는 방식

  ```css
  <head>
      <link rel="stylesheet" href="./main.css" />
  </head>
  <body>
      <div>link</div>
  </body>

  /*main.css*/
  @import url("./common.css");

  /*common.css*/
  div {
    color:red;
  }
  ```

  - 직렬 호출, 순차적인 불러오기로 주의하여 사용

### 선택자(Selector) : 기본 선택자(Basic Selectors)

- 전체 선택자(Universal Selector) : 요소 내부의 모든 요소를 선택

  ```css
  * {
    color: red;
  }
  ```

- 태그 선택자(Type Selector) : 태그 이름이 `<E>`인 모든 요소 선택

  ```css
  li {
    color: red;
  }
  ```

- 클래스 선택자(Class Selector) : HTML `class 속성`의 값이 `E`인 모든 요소 선택

  ```css
  .apple {
    color: red;
  }
  ```

  ```html
  <div class="apple">class1</div>
  <div class="apple">class2</div>
  <div class="apple">class3</div>
  ```

- 아이디 선택자(Id Selector) : HTML `id 속성`의 값이 `E`인 단일 요소 선택

  ```css
  #apple {
    color: red;
  }
  ```

  ```html
  <div class="apple">id1</div>

  <div id="apple" class="apple">id2</div>
  ```

### 선택자(Selector) : 복합 선택자(Combinators)

- 일치 선택자(Basic Combinator) : `E`와 `F`를 동시에 만족하는 요소 선택

  ```css
  span.apple {
    color: red;
  }
  ```

  ```html
  <div class="apple">basic1</div>

  <span class="apple">basic2</span>
  ```

- 자식 선택자(Child Combinator) : `E`의 `자식 요소 F`를 선택

  ```css
  div > .apple {
    color: red;
  }
  ```

  ```html
  <span class="apple">child1</span>

  <div>
    <span class="apple">child2</span>
  </div>
  ```

- 후손(하위) 선택자(Descendant Combinator) : `E`의 `후손(하위) 요소 F`를 모두 선택

  - `띄어쓰기`가 선택자의 기호로 사용된다.

    ```css
    div .apple {
      color: red;
    }
    ```

    ```html
    <div>
      <div class="apple">div1</div>
      <span class="apple">span1</span>
      <p class="apple">p1</p>
    </div>
    ```

- 인접 형제 선택자(Adjacent Sibling Combinator) : `E`의 `다음 형제 요소 F` 하나만 선택

  ```css
  .apple + span {
    color: red;
  }
  ```

  ```html
  <div class="apple">div1</div>

  <span>span1</span>
  ```

- 일반 형제 선택자(General Sibling Combinator) : `E`의 `다음 형제 요소 F` 모두 선택

```css
.apple ~ span {
  color: red;
}
```

```html
<span>span1</span>

<div class="apple">div1</div>

<span>span2</span>
<span>span3</span>
```

### 가상 클래스 선택자(Pseudo-Classes Selectors)

- hover : `E`에 마우스(포인터)가 올라가 있는 동안에만 `E` 선택

  ```css
  a:hover {
    font-weight: bold;
  }
  ```

- active : `E`를 마우스로 클릭하는 동안에만 `E` 선택

  ```css
  div:active {
    width: 200px;
  }
  ```

- focus : `E`가 포커스 된 동안에만 `E`선택

  - 대화형 콘텐츠에서 사용 가능(input, img, tabindex)

    ```css
    input:focus {
      border-color: red;
      width: 200px;
    }
    ```

- first child : `E`가 형제 요소 중 첫번째 요소라면 선택

  ```css
  .fruits li:first-child {
    color: red;
  }

  /* 이것도 가능함 */
  /* 후손의 모든 첫번째 요소 선택*/
  .fruits :first-child {
    color: blue;
  }
  ```

  ```html
  <ul class="fruits">
    <!-- 선택 -->
    <li>사과</li>
    <li>포도</li>
    <li>오렌지</li>
  </ul>
  ```

- last child : `E`가 형제 요소 중 마지막 요소라면 선택

  ```css
  .fruits li:last-child {
    color: red;
  }
  ```

  ```html
  <ul class="fruits">
    <li>사과</li>
    <li>포도</li>
    <!-- 선택 -->
    <li>오렌지</li>
  </ul>
  ```

- nth-child : `E`가 형제 요소 중 n번째 요소라면 선택(n 키워드는 0부터 해석(Zero-base))

  - 자연수

    ```css
    .fruits li:nth-child(2) {
      color: red;
    }
    ```

    ```html
    <ul class="fruits">
      <li>사과</li>
      <!-- 선택 -->
      <li>포도</li>
      <li>오렌지</li>
      <li>바나나</li>
    </ul>
    ```

  - `자연수 * n` : `자연수 * n` 요소들 선택

    ```css
    .fruits li:nth-child(2n) {
      color: red;
    }
    ```

    ```html
    <ul class="fruits">
      <li>사과</li>
      <!-- 선택 -->
      <li>포도</li>
      <li>오렌지</li>
      <!-- 선택 -->
      <li>바나나</li>
    </ul>
    ```

  - `자연수 + n` : n 이후 요소들 선택

    ```css
    .fruits li:nth-child(n + 3) {
      color: red;
    }
    ```

    ```html
    <ul class="fruits">
      <li>사과</li>
      <li>포도</li>
      <!-- 선택 -->
      <li>오렌지</li>
      <!-- 선택 -->
      <li>바나나</li>
    </ul>
    ```

  - n 번째 자식 요소가 조건에 부합되지 않으면 선택되지 않는다.

    ```css
    .fruits p:nth-child(1) {
      color: red;
    }
    ```

    ```html
    <div class="fruits">
      <div>사과</div>
      <p>포도</p>
      <p>오렌지</p>
      <span>바나나</span>
    </div>
    ```

- nth-of-type : `E`의 타입(태그 이름)과 동일한 타입인 형제 요소 중 `E`가 n번째 요소라면 선택(n 키워드는 0부터 해석(Zero-base))

  ```css
  .fruits li:nth-of-type(1) {
    color: red;
  }
  ```

  ```html
  <ul class="fruits">
    <li class="red">사과</li>
    <li>포도</li>
    <li class="red">딸기</li>
    <li>바나나</li>
  </ul>
  ```

- 부정 선택자(Negation Selector) : `S`가 아닌 `E` 선택

  ```css
  .fruits li:not('apple') {
    color: red;
  }
  ```

  ```html
  <ul class="fruits">
    <li class="apple">사과</li>
    <li>포도</li>
    <li>딸기</li>
    <li>바나나</li>
  </ul>
  ```

### 가상 요소 선택자(Pseudo-Elements Selectors)

- before : `E` 요소 내부의 앞에, 내용(content)을 삽입
  - 가상 클래스는 `:` 하나, 가상 요소는 `::` 두개
