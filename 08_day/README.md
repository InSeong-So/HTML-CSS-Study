# 8일차

## SCSS(Sass) 설치

- [온라인 변환 사이트(sassmeister)](https://www.sassmeister.com/)

- node 모듈을 통한 변환

  ```sh
  npm init -y

  npm i -D parcel-bundler

  npx parcel 프로그램명
  ```

## 주석(Comment)

```scss
// 컴파일되지 않는 주석
/* 컴파일 되는 주석 */
```

## 데이터 유형(Data Types)

| 데이터   | 설명                                  | 예시                                     |
| -------- | ------------------------------------- | ---------------------------------------- |
| Numbers  | 숫자                                  | 1, .82, 20px, 2em…                       |
| Strings  | 문자                                  | bold, relative, "/images/a.png", "dotum" |
| Colors   | 색상 표현                             | red, blue, #FFFF00, rgba(255,0,0,.5)     |
| Booleans | 논리                                  | true, false                              |
| Nulls    | 아무것도 없음                         | null                                     |
| Lists    | 공백이나 ,로 구분된 값의 목록         | (apple, orange, banana), apple orange    |
| Maps     | Lists와 유사하나 값이 Key: Value 형태 | (apple: a, orange: o, banana: b)         |

- 특징
  - Numbers: 숫자에 단위가 있거나 없다.
  - Strings: 문자에 따옴표가 있거나 없다.
  - Nulls: 속성값으로 null이 사용되면 컴파일하지 않는다.
  - Lists: ()를 붙이거나 붙이지 않는다.
  - Maps: ()를 꼭 붙여야 한다.

## 중첩(Nesting)

```scss
.section {
  width: 100%;
  .list {
    padding: 20px;
    li {
      float: left;
    }
  }
}
```

### Ampersand(상위 선택자 참조)

- 컴파일 전

  ```scss
  .btn {
    position: absolute;
    &.active {
      color: red;
    }
  }

  .list {
    li {
      &:last-child {
        margin-right: 0;
      }
    }
  }
  /* ============================= */
  .fs {
    &-small {
      font-size: 12px;
    }
    &-medium {
      font-size: 14px;
    }
    &-large {
      font-size: 16px;
    }
  }
  ```

- 컴파일 후

  ```css
  .btn {
    position: absolute;
  }
  .btn.active {
    color: red;
  }
  .list li:last-child {
    margin-right: 0;
  }
  /* ============================= */
  .fs-small {
    font-size: 12px;
  }
  .fs-medium {
    font-size: 14px;
  }
  .fs-large {
    font-size: 16px;
  }
  ```

### @at-root (중첩 벗어나기)

> 중첩 안에서 생성하되 중첩 밖에서 사용해야 하는 경우 매우 유용

- 컴파일 전

  ```scss
  /* 에러가 나는 예시 */
  .list {
    $w: 100px;
    $h: 50px;
    li {
      width: $w;
      height: $h;
    }
  }

  // Error
  .box {
    width: $w;
    height: $h;
  }
  ```

  ```scss
  /* 중첩 벗어나기를 활용한 경우 */
  .list {
    $w: 100px;
    $h: 50px;
    li {
      width: $w;
      height: $h;
    }
    @at-root .box {
      width: $w;
      height: $h;
    }
  }
  ```

- 컴파일 후

  ```css
  .list li {
    width: 100px;
    height: 50px;
  }
  .box {
    width: 100px;
    height: 50px;
  }
  ```

### 중첩된 속성

> font-, margin- 등과 같이 동일한 네임 스페이스를 가지는 속성을 활용

- 컴파일 전

  ```scss
  .box {
    font: {
      weight: bold;
      size: 10px;
      family: sans-serif;
    }
    margin: {
      top: 10px;
      left: 20px;
    }
    padding: {
      bottom: 40px;
      right: 30px;
    }
  }
  ```

- 컴파일 후

  ```css
  .box {
    font-weight: bold;
    font-size: 10px;
    font-family: sans-serif;
    margin-top: 10px;
    margin-left: 20px;
    padding-bottom: 40px;
    padding-right: 30px;
  }
  ```

## 변수(Variables)

> 반복적으로 사용되는 값을 `$변수명`으로 지정

- 컴파일 전

  ```scss
  $color-primary: #e96900;
  $url-images: '/assets/images/';
  $w: 200px;

  .box {
    width: $w;
    margin-left: $w;
    background: $color-primary url($url-images + 'bg.jpg');
  }
  ```

- 컴파일 후
  ```css
  .box {
    width: 200px;
    margin-left: 200px;
    background: #e96900 url('/assets/images/bg.jpg');
  }
  ```

### 변수 유효범위(Variable Scope)

> 선언된 블록({}) 내에서만 유효

```scss
.box1 {
  $color: #111;
  background: $color;
}

// Error
.box2 {
  background: $color;
}
```

### 변수 재 할당(Variable Reassignment)

- 컴파일 전

  ```scss
  $red: #ff0000;
  $blue: #0000ff;

  $color-primary: $blue;
  $color-danger: $red;

  .box {
    color: $color-primary;
    background: $color-danger;
  }
  ```

- 컴파일 후

  ```css
  .box {
    color: #0000ff;
    background: #ff0000;
  }
  ```

### `!global` (전역 설정)

> 변수의 유효범위를 전역(Global)로 설정

- 컴파일 전

  ```scss
  /* 기존에 사용하던 같은 이름의 변수가 있을 경우 값이 덮어져 사용된다. */
  .box1 {
    $color: #111 !global;
    background: $color;
  }
  .box2 {
    background: $color;
  }
  ```

- 컴파일 후

  ```scss
  .box1 {
    background: #111;
  }
  .box2 {
    background: #111;
  }
  ```

### `!default` (초깃값 설정)

> 할당되지 않은 변수의 초깃값 설정

- `변수와 값을 설정하겠지만, 혹시 기존 변수가 있을 경우는 현재 설정하는 변수의 값은 사용하지 않겠다`

- 컴파일 전

  ```scss
  $color-primary: red;

  .box {
    $color-primary: blue !default;
    background: $color-primary;
  }
  ```

- 컴파일 후

  ```css
  .box {
    background: red;
  }
  ```

### `#{}` (문자 보간)

> 코드의 어디든지 변수 값을 넣을 수 있다.

- 컴파일 전

  ```scss
  /* Sass의 내장 함수 unquote()는 문자에서 따옴표를 제거한다. */
  $family: unquote('Droid+Sans');
  @import url('http://fonts.googleapis.com/css?family=#{$family}');
  ```

- 컴파일 후

  ```css
  @import url('http://fonts.googleapis.com/css?family=Droid+Sans');
  ```

## 가져오기(Import)

> `@import`로 외부에서 가져온 Sass 파일은 모두 단일 CSS 출력 파일로 병합된다.
> 가져온 파일에 정의된 모든 변수 또는 Mixins 등을 주 파일에서 사용할 수 있다.

- CSS @import 규칙대로 컴파일 되는 순서

  1. 파일 확장자가 .css일 때
  2. 파일 이름이 http://로 시작하는 경우
  3. url()이 붙었을 경우
  4. 미디어쿼리가 있는 경우

  ```scss
  @import 'hello.css';
  @import 'http://hello.com/hello';
  @import url(hello);
  @import 'hello' screen;
  ```

### 여러 파일 가져오기

> `,`로 구분하여 하나의 `@import`로 여러 파일 가져오기

```scss
@import 'header', 'footer';
```

### 파일 분할(Partials)

- 프로젝트 규모가 커지면 파일들을 header나 side-menu 같이 각 기능과 부분으로 나눠 유지보수가 쉽도록 관리하게 된다.
  - 이 경우 파일이 점점 많아지는데, 모든 파일이 컴파일 시 각각의 ~.css 파일로 나눠서 저장된다면 관리나 성능 차원에서 문제가 될 수 있으므로 Sass는 Partials 기능을 지원한다.
- 파일 이름 앞에 `_`를 붙여(`_header.scss`와 같이) @import로 가져오면 컴파일 시 ~.css 파일로 컴파일하지 않는다.

```bash
Sass-App
  # ...
  ├─scss
  │  ├─_header.scss
  │  ├─_side-menu.scss
  │  └─main.scss
  # ...
```

```scss
// main.scss
@import 'header', 'side-menu';
```

```scss
$ node-sass scss --output css
```

```bash
Sass-App
  # ...
  ├─css
  │  └─main.css  # main + header + side-menu
  ├─scss
  │  ├─header.scss
  │  ├─side-menu.scss
  │  └─main.scss
  # ...
```

- Webpack이나 Parcel, Gulp 같은 일반적인 빌드툴에서는 Partials 기능을 사용하지 않아도 설정된 값에 따라 빌드되지만 되도록 `_`를 사용할 것을 권장한다.

## 연산(Operations)

> 레이아웃 작업시 상황에 맞게 크기를 계산을 하거나 정해진 값을 나눠서 작성할 경우 유용

- 산술 연산자

  | 종류 | 설명   | 주의사항                             |
  | ---- | ------ | ------------------------------------ |
  | +    | 더하기 |                                      |
  | -    | 빼기   |                                      |
  | \*   | 곱하기 | 하나 이상의 값이 반드시 숫자(Number) |
  | /    | 나누기 | 오른쪽 값이 반드시 숫자(Number)      |
  | %    | 나머지 |                                      |

- 비교 연산자

  | 종류 | 설명                            |
  | ---- | ------------------------------- |
  | ==   | 동등                            |
  | !=   | 부등                            |
  | <    | 대소 / 보다 작은                |
  | >    | 대소 / 보다 큰                  |
  | <=   | 대소 및 동등 / 보다 작거나 같은 |
  | >=   | 대소 및 동등 / 보다 크거나 같은 |

- 논리 연산자

  | 종류 | 설명   |
  | ---- | ------ |
  | and  | 그리고 |
  | or   | 또는   |
  | not  | 부정   |

### 숫자(Numbers)

- 상대적 단위 연산

  - 일반적으론 절댓값을 나타내는 px 단위로 연산을 하지만 상대적 단위(%, em, vw 등)의 연산의 경우 CSS `calc()`로 연산해야 한다.

  ```scss
  width: 50% - 20px; // 단위 모순 에러(Incompatible units error)
  width: calc(50% - 20px); // 연산 가능
  ```

- 나누기 연산의 주의사항

  - CSS는 속성 값의 숫자를 분리하는 방법으로 `/`를 허용하기 때문에 `/`가 나누기 연산으로 사용되지 않을 수 있다.
  - `font: 16px / 22px serif;`의 경우 `font-size: 16px`와 `line-height: 22px`의 속성값 분리를 위해서 /를 사용하면 연산 되지 않고 그대로 컴파일된다.

  ```scss
  div {
    $x: 100px;
    width: $x / 2; // 변수에 저장된 값을 나누기
    height: (100px / 2); // 괄호로 묶어서 나누기
    font-size: 10px + 12px / 3; // 더하기 연산과 같이 사용
    margin: 30px / 2; // 나누기
  }
  ```

  ```css
  div {
    width: 50px; /* OK */
    height: 50px; /* OK */
    font-size: 14px; /* OK */
    margin: 30px / 2; /* ?? */
  }
  ```

  - 즉, `/`를 나누기 연산 기능으로 사용하려면 다음과 같은 조건을 충족해야 한다.

    1. 값 또는 그 일부가 변수에 저장되거나 함수에 의해 반환되는 경우
    2. 값이 ()로 묶여있는 경우
    3. 값이 다른 산술 표현식의 일부로 사용되는 경우

### 문자(Strings)

1. 문자 연산에는 +가 사용된다.
2. 문자 연산의 결과는 첫 번째 피연산자를 기준으로 한다.
3. 첫 번째 피연산자에 따옴표가 붙어있다면 연산 결과를 따옴표로 묶는다.
   - 첫 번째 피연산자에 따옴표가 붙어있지 않다면 연산 결과도 따옴표를 처리하지 않는다.

- 컴파일 전

  ```scss
  div::after {
    content: 'Hello ' + World;
    flex-flow: row + '-reverse' + ' ' + wrap;
  }
  ```

- 컴파일 후

  ```css
  div::after {
    content: 'Hello World';
    flex-flow: row-reverse wrap;
  }
  ```

### 색상(Colors)

- 컴파일 전

  ```scss
  div {
    color: #123456 + #345678;
    // R: 12 + 34 = 46
    // G: 34 + 56 = 8a
    // B: 56 + 78 = ce
    background: rgba(50, 100, 150, 0.5) + rgba(10, 20, 30, 0.5);
    // R: 50 + 10 = 60
    // G: 100 + 20 = 120
    // B: 150 + 30 = 180
    // A: Alpha channels must be equal
  }
  ```

- 컴파일 후

  ```css
  div {
    color: #468ace;
    background: rgba(60, 120, 180, 0.5);
  }
  ```

- RGBA에서 Alpha 값은 연산되지 않으며 서로 동일해야 다른 값의 연산이 가능하다.

  - Alpha 값을 연산하기 위한 다음과 같은 색상 함수(Color Functions)를 사용할 수 있다.

    ```scss
    $color: rgba(10, 20, 30, 0.5);
    div {
      color: opacify($color, 0.3); // 30% 더 불투명하게 / 0.5 + 0.3
      background-color: transparentize(
        $color,
        0.2
      ); // 20% 더 투명하게 / 0.5 - 0.2
    }
    ```

    ```css
    div {
      color: rgba(10, 20, 30, 0.8);
      background-color: rgba(10, 20, 30, 0.3);
    }
    ```

### 논리(Boolean)

> 자바스크립트 문법의 `&&`, `||`, `!`와 같은 기능

- 컴파일 전

  ```scss
  $width: 90px;
  div {
    @if not($width > 100px) {
      height: 300px;
    }
  }
  ```

- 컴파일 후

  ```css
  div {
    height: 300px;
  }
  ```

## 재활용(Mixins)

> 스타일 시트 전체에서 재사용 할 CSS 선언 그룹을 정의하는 기능
>
> - 선언하기(@mixin)와 포함하기(@include), 즉 만들어서(선언), 사용(포함)하는 것

### @mixin

> @mixin 지시어를 이용하여 스타일을 정의

```scss
// SCSS
@mixin 믹스인이름 {
  스타일;
}

// Sass
=믹스인이름
  스타일
```

```css
// SCSS
@mixin large-text {
  font-size: 22px;
  font-weight: bold;
  font-family: sans-serif;
  color: orange;
}

// Sass
=large-text
  font-size: 22px
  font-weight: bold
  font-family: sans-serif
  color: orange
```

- Mixin은 선택자를 포함하며 상위(부모) 요소 참조(& 같은)도 할 수 있다.

  ```scss
  @mixin large-text {
    font: {
      size: 22px;
      weight: bold;
      family: sans-serif;
    }
    color: orange;

    &::after {
      content: '!!';
    }

    span.icon {
      background: url('/images/icon.png');
    }
  }
  ```

### @include

> 선언된 Mixin을 사용(포함)하기 위함

```scss
// SCSS
@include 믹스인이름;

// Sass
+믹스인이름
```

- 컴파일 전

  ```scss
  // SCSS
  h1 {
  @include large-text;
  }
  div {
  @include large-text;
  }

  // Sass
  h1
  +large-text
  div
  +large-text
  ```

- 컴파일 후

  ```css
  h1 {
    font-size: 22px;
    font-weight: bold;
    font-family: sans-serif;
    color: orange;
  }
  h1::after {
    content: '!!';
  }
  h1 span.icon {
    background: url('/images/icon.png');
  }

  div {
    font-size: 22px;
    font-weight: bold;
    font-family: sans-serif;
    color: orange;
  }
  div::after {
    content: '!!';
  }
  div span.icon {
    background: url('/images/icon.png');
  }
  ```

### 인수(Arguments)

> Mixin은 함수(Functions)처럼 인수(Arguments)를 가질 수 있다.

```scss
// SCSS
@mixin 믹스인이름($매개변수) {
  스타일;
}
@include 믹스인이름(인수);

// Sass
=믹스인이름($매개변수)
  스타일

+믹스인이름(인수)
```

- 컴파일 전

  ```scss
  @mixin dash-line($width, $color) {
    border: $width dashed $color;
  }

  .box1 {
    @include dash-line(1px, red);
  }
  .box2 {
    @include dash-line(4px, blue);
  }
  ```

- 컴파일 후

  ```css
  .box1 {
    border: 1px dashed red;
  }
  .box2 {
    border: 4px dashed blue;
  }
  ```

- 인수의 기본값 설정

  - 인수(argument)는 기본값(default value)을 가질 수 있으며 @include 포함 단계에서 별도의 인수가 전달되지 않으면 기본값이 사용된다.

  ```scss
  @mixin 믹스인이름($매개변수: 기본값) {
  스타일;
  }
  ```

  ```scss
  @mixin dash-line($width: 1px, $color: black) {
    border: $width dashed $color;
  }

  .box1 {
    @include dash-line;
  }
  .box2 {
    @include dash-line(4px);
  }
  ```

  ```css
  .box1 {
    border: 1px dashed black;
  }
  .box2 {
    border: 4px dashed black;
  }
  ```

- 키워드 인수(Keyword Arguments)

  ```scss
  @mixin 믹스인이름($매개변수A: 기본값, $매개변수B: 기본값) {
  스타일;
  }

  @include 믹스인이름($매개변수B: 인수);
  ```

  - Mixin에 전달할 인수를 입력할 때 명시적으로 키워드(변수)를 입력하여 작성할 수 있다.
  - 별도의 인수 입력 순서를 필요로 하지 않아 편리하게 작성할 수 있으며, 작성하지 않은 인수가 적용될 수 있도록 기본값을 설정해 주는 것이 좋다.

  ```scss
  @mixin position($p: absolute, $t: null, $b: null, $l: null, $r: null) {
    position: $p;
    top: $t;
    bottom: $b;
    left: $l;
    right: $r;
  }

  .absolute {
    // 키워드 인수로 설정할 값만 전달
    @include position($b: 10px, $r: 20px);
  }
  .fixed {
    // 인수가 많아짐에 따라 가독성을 확보하기 위해 줄바꿈
    @include position(fixed, $t: 30px, $r: 40px);
  }
  ```

  ```css
  .absolute {
    position: absolute;
    bottom: 10px;
    right: 20px;
  }
  .fixed {
    position: fixed;
    top: 30px;
    right: 40px;
  }
  ```

- 가변 인수(Variable Arguments)

  - 입력할 인수의 개수가 불확실한 경우 사용한다.
  - 매개변수 뒤에 `...`을 붙여 사용하는 경우

    ```scss
    @mixin 믹스인이름($매개변수...) {
    스타일;
    }

    @include 믹스인이름(인수A, 인수B, 인수C);
    ```

    ```scss
    // 인수를 순서대로 하나씩 전달 받다가, 3번째 매개변수($bg-values)는 인수의 개수에 상관없이 받음
    @mixin bg($width, $height, $bg-values...) {
      width: $width;
      height: $height;
      background: $bg-values;
    }

    div {
      // 위의 Mixin(bg) 설정에 맞게 인수를 순서대로 전달하다가 3번째 이후부터는 개수에 상관없이 전달
      @include bg(
        100px,
        200px,
        url('/images/a.png') no-repeat 10px 20px,
        url('/images/b.png') no-repeat,
        url('/images/c.png')
      );
    }
    ```

    ```css
    div {
      width: 100px;
      height: 200px;
      background: url('/images/a.png') no-repeat 10px 20px, url('/images/b.png')
          no-repeat, url('/images/c.png');
    }
    ```

  - 가변인수 뒤에 `...`을 붙여 사용하는 경우

    ```scss
    @mixin font(
      $style: normal,
      $weight: normal,
      $size: 16px,
      $family: sans-serif
    ) {
      font: {
        style: $style;
        weight: $weight;
        size: $size;
        family: $family;
      }
    }
    ```

    ```css
    div {
      // 매개변수 순서와 개수에 맞게 전달
      $font-values: italic, bold, 16px, sans-serif;
      @include font($font-values...);
    }
    span {
      // 필요한 값만 키워드 인수로 변수에 담아 전달
      $font-values: (
        style: italic,
        size: 22px
      );
      @include font($font-values...);
    }
    a {
      // 필요한 값만 키워드 인수로 전달
      @include font((weight: 900, family: monospace)...);
    }
    div {
      font-style: italic;
      font-weight: bold;
      font-size: 16px;
      font-family: sans-serif;
    }
    span {
      font-style: italic;
      font-weight: normal;
      font-size: 22px;
      font-family: sans-serif;
    }
    a {
      font-style: normal;
      font-weight: 900;
      font-size: 16px;
      font-family: monospace;
    }
    ```

### @content

> 선언된 Mixin에 @content이 포함되어 있다면 해당 부분에 원하는 `스타일 블록`을 전달

- 기존 Mixin이 가지고 있는 기능에 선택자나 속성 등을 추가할 수 있다.

  ```scss
  @mixin 믹스인이름() {
      스타일;
      @content;
  }

  @include 믹스인이름() {
      // 스타일 블록
      스타일;
  }
  ```

- 컴파일 전

  ```scss
  @mixin icon($url) {
    &::after {
      content: $url;
      @content;
    }
  }
  .icon1 {
    // icon Mixin의 기존 기능만 사용
    @include icon('/images/icon.png');
  }
  .icon2 {
    // icon Mixin에 스타일 블록을 추가하여 사용
    @include icon('/images/icon.png') {
      position: absolute;
    }
  }
  ```

- 컴파일 후

  ```scss
  .icon1::after {
    content: '/images/icon.png';
  }
  .icon2::after {
    content: '/images/icon.png';
    position: absolute;
  }
  ```

- Mixin에게 전달된 스타일 블록은 Mixin의 범위가 아니라 스타일 블록이 정의된 범위에서 평가된다.

  - 즉, Mixin의 매개변수는 전달된 스타일 블록 안에서 사용되지 않고 전역 값으로 해석된다.
  - 전역 변수(Global variables)와 지역 변수(Local variables)를 생각하여 이해할 것

  ```scss
  $color: red;

  @mixin colors($color: blue) {
    // Mixin의 범위
    @content;
    background-color: $color;
    border-color: $color;
  }

  div {
    @include colors() {
      // 스타일 블록이 정의된 범위
      color: $color;
    }
  }
  ```

  ```css
  div {
    color: red;
    background-color: blue;
    border-color: blue;
  }
  ```

## ~~확장(Extend)~~

## 함수(Functions)

> 자신의 함수를 정의하여 사용

- Mixin은 지정한 스타일(Style)을 반환하지만 함수는 보통 연산된(Computed) 특정 값을 @return 지시어를 통해 반환한다.

  ```scss
  /* 선언 */
  // Mixins
  @mixin 믹스인이름($매개변수) {
    스타일;
  }

  // Functions
  @function 함수이름($매개변수) {
    @return 값
  }

  /* 사용 */
  // Mixin
  @include 믹스인이름(인수);

  // Functions
  함수이름(인수)
  ```

- 컴파일 전

  ```scss
  $max-width: 980px;

  @function columns($number: 1, $columns: 12) {
    @return $max-width * ($number / $columns);
  }

  .box_group {
    width: $max-width;

    .box1 {
      width: columns(); // 1
    }
    .box2 {
      width: columns(8);
    }
    .box3 {
      width: columns(3);
    }
  }
  ```

- 컴파일 후

  ```css
  .box_group {
    /* 총 너비 */
    width: 980px;
  }
  .box_group .box1 {
    /* 총 너비의 약 8.3% */
    width: 81.66667px;
  }
  .box_group .box2 {
    /* 총 너비의 약 66.7% */
    width: 653.33333px;
  }
  .box_group .box3 {
    /* 총 너비의 25% */
    width: 245px;
  }
  ```

- 함수는 @include 같은 별도의 지시어 없이 사용하기 때문에 내가 지정한 함수와 내장 함수(Built-in Functions)의 이름이 충돌할 수 있으므로 별도의 접두어를 붙여주는 것이 좋다.

  ```scss
  // 내가 정의한 함수
  @function extract-red($color) {
    // 내장 함수
    @return rgb(red($color), 0, 0);
  }

  div {
    color: extract-red(#d55a93);
  }
  ```

## 조건과 반복(Control Directives / Expressions)

### if (함수)

> 조건의 값(true, false)에 따라 두 개의 표현식 중 하나만 반환

- 조건부 삼항 연산자(conditional ternary operator)와 비슷하다.

  1. 조건의 값이 true이면 표현식1 실행
  2. 조건의 값이 false이면 표현식2 실행

```scss
if(조건, 표현식1, 표현식2)
```

- 컴파일 전

  ```scss
  $width: 555px;
  div {
    width: if($width > 300px, $width, null);
  }
  ```

- 컴파일 후

  ```css
  div {
    width: 555px;
  }
  ```

### @if (지시어)

> 조건에 따른 분기 처리가 가능하며, if 문(if statements)과 유사

- 같이 사용할 수 있는 지시어는 @else, if가 있으며 추가 지시어를 사용하면 좀 더 복잡한 조건문을 작성할 수 있다.

```scss
// @if
@if (조건) {
  /* 조건이 참일 때 구문 */
}

// @if @else
@if (조건) {
  /* 조건이 참일 때 구문 */
} @else {
  /* 조건이 거짓일 때 구문 */
}

// @if @else if
@if (조건1) {
  /* 조건1이 참일 때 구문 */
} @else if (조건2) {
  /* 조건2가 참일 때 구문 */
} @else {
  /* 모두 거짓일 때 구문 */
}
```

- 조건에 ()는 생략이 가능하다.

  ```scss
  $bg: true;
  div {
    @if $bg {
      background: url('/images/a.jpg');
    }
  }
  ```

  - 컴파일 전

    ```scss
    $color: orange;
    div {
      @if $color == strawberry {
        color: #fe2e2e;
      } @else if $color == orange {
        color: #fe9a2e;
      } @else if $color == banana {
        color: #ffff00;
      } @else {
        color: #2a1b0a;
      }
    }
    ```

  - 컴파일 후

    ```css
    div {
      color: #fe9a2e;
    }
    ```

- 조건에 논리 연산자 and, or, not을 사용할 수 있다.

  - 컴파일 전

    ```scss
    @function limitSize($size) {
      @if $size >= 0 and $size <= 200px {
        @return 200px;
      } @else {
        @return 800px;
      }
    }

    div {
      width: limitSize(180px);
      height: limitSize(340px);
    }
    ```

  - 컴파일 후

    ```css
    div {
      width: 200px;
      height: 800px;
    }
    ```

- 종합 예제

  - 컴파일 전

    ```scss
    @mixin pCenter($w, $h, $p: absolute) {
      @if $p ==
        absolute or
        $p ==
        fixed or not
        $p ==
        relative or not
        $p ==
        static
      {
        width: if(unitless($w), #{$w}px, $w);
        height: if(unitless($h), #{$h}px, $h);
        position: $p;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
      }
    }

    .box1 {
      @include pCenter(10px, 20px);
    }
    .box2 {
      @include pCenter(50, 50, fixed);
    }
    .box3 {
      @include pCenter(100, 200, relative);
    }
    ```

  - 컴파일 후

    ```css
    .box1 {
      width: 10px;
      height: 20px;
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      margin: auto;
    }

    .box2 {
      width: 50px;
      height: 50px;
      position: fixed;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      margin: auto;
    }
    ```

### @for

> 스타일을 반복적으로 출력

- @for는 through를 사용하는 형식과 to를 사용하는 형식으로 나뉘며 종료 조건이 해석되는 방식이 다르다.
  - 변수는 관례상 $i를 사용한다.

```scss
// through
// 종료 만큼 반복
@for $변수 from 시작 through 종료 {
  // 반복 내용
}

// to
// 종료 직전까지 반복
@for $변수 from 시작 to 종료 {
  // 반복 내용
}
```

- 컴파일 전

  ```scss
  // 1부터 3번 반복
  @for $i from 1 through 3 {
    .through:nth-child(#{$i}) {
      width: 20px * $i;
    }
  }

  // 1부터 3 직전까지만 반복(2번 반복)
  @for $i from 1 to 3 {
    .to:nth-child(#{$i}) {
      width: 20px * $i;
    }
  }
  ```

- 컴파일 후

  ```css
  .through:nth-child(1) {
    width: 20px;
  }
  .through:nth-child(2) {
    width: 40px;
  }
  .through:nth-child(3) {
    width: 60px;
  }

  .to:nth-child(1) {
    width: 20px;
  }
  .to:nth-child(2) {
    width: 40px;
  }
  ```

  - to는 주어진 값 직전까지만 반복해야할 경우 유용할 수 있으나 :nth-child()에서 특히 유용하게 사용되는 @for는 일반적으로 through를 사용하길 권장한다.

### @each

> List와 Map 데이터를 반복할 때 사용하며 for in 문과 유사

```scss
@each $변수 in 데이터 {
  // 반복 내용
}
```

- 컴파일 전

  ```scss
  // List Data
  $fruits: (apple, orange, banana, mango);

  .fruits {
    @each $fruit in $fruits {
      li.#{$fruit} {
        background: url('/images/#{$fruit}.png');
      }
    }
  }
  ```

- 컴파일 후

  ```css
  .fruits li.apple {
    background: url('/images/apple.png');
  }
  .fruits li.orange {
    background: url('/images/orange.png');
  }
  .fruits li.banana {
    background: url('/images/banana.png');
  }
  .fruits li.mango {
    background: url('/images/mango.png');
  }
  ```

- 반복마다 index 값이 필요한 경우 내장 함수 index()를 사용한다.

  ```scss
  $fruits: (apple, orange, banana, mango);

  .fruits {
    @each $fruit in $fruits {
      $i: index($fruits, $fruit);
      li:nth-child(#{$i}) {
        left: 50px * $i;
      }
    }
  }
  ```

  ```css
  .fruits li:nth-child(1) {
    left: 50px;
  }
  .fruits li:nth-child(2) {
    left: 100px;
  }
  .fruits li:nth-child(3) {
    left: 150px;
  }
  .fruits li:nth-child(4) {
    left: 200px;
  }
  ```

- 동시에 여러 개의 List 데이터를 반복 처리할 수도 있으나 각 데이터의 Length가 같아야 한다.

  ```scss
  $apple: (apple, korea);
  $orange: (orange, china);
  $banana: (banana, japan);

  @each $fruit, $country in $apple, $orange, $banana {
    .box-#{$fruit} {
      background: url('/images/#{$country}.png');
    }
  }
  ```

  ```css
  .box-apple {
    background: url('/images/korea.png');
  }
  .box-orange {
    background: url('/images/china.png');
  }
  .box-banana {
    background: url('/images/japan.png');
  }
  ```

- Map 데이터를 반복할 경우 하나의 데이터에 두 개의 변수가 필요하다.

  ```scss
  @each $key변수, $value변수 in 데이터 {
    // 반복 내용
  }
  ```

  ```scss
  $fruits-data: (
    apple: korea,
    orange: china,
    banana: japan,
  );

  @each $fruit, $country in $fruits-data {
    .box-#{$fruit} {
      background: url('/images/#{$country}.png');
    }
  }
  ```

  ```css
  .box-apple {
    background: url('/images/korea.png');
  }
  .box-orange {
    background: url('/images/china.png');
  }
  .box-banana {
    background: url('/images/japan.png');
  }
  ```

### ~~@while~~

## 내장 함수(Built-in Functions)

> [Sass Built-in Functions](https://poiemaweb.com/sass-built-in-function)

- []는 선택 가능한 인수(argument)
- Zero-based numbering을 사용하지 않는다.

### 색상(RGB / HSL / Opacity) 함수

- mix($color1, $color2) : 두 개의 색을 섞는다.

- lighten($color, $amount) : 더 밝은색을 만든다.

- darken($color, $amount) : 더 어두운색을 만든다.

- saturate($color, $amount) : 색상의 채도를 올린다.

- desaturate($color, $amount) : 색상의 채도를 낮춘다.

- grayscale($color) : 색상을 회색으로 변환한다.

- invert($color) : 색상을 반전시킨다.

- rgba($color, $alpha) : 색상의 투명도를 변경한다.

- opacify($color, $amount) / fade-in($color, $amount) : 색상을 더 불투명하게 만든다.

- transparentize($color, $amount) / fade-out($color, $amount) : 색상을 더 투명하게 만든다.

### 문자(String) 함수

- unquote($string) : 문자에서 따옴표를 제거한다.

- quote($string) : 문자에 따옴표를 추가한다.

- str-insert($string, $insert, $index) : 문자의 index번째에 특정 문자를 삽입한다.

- str-index($string, $substring) : 문자에서 특정 문자의 첫 index를 반환한다.

- str-slice($string, $start-at, [$end-at]) : 문자에서 특정 문자(몇 번째 글자부터 몇 번째 글자까지)를 추출한다.

- to-upper-case($string) : 문자를 대문자를 변환한다.

- to-lower-case($string) : 문자를 소문자로 변환한다.

### 숫자(Number) 함수

- percentage($number) : 숫자(단위 무시)를 백분율로 변환한다.

- round($number) : 정수로 반올림한다.

- ceil($number) : 정수로 올림한다.

- floor($number) : 정수로 내림(버림)한다.

- abs($number) : 숫자의 절대 값을 반환한다.

- min($numbers…) : 숫자 중 최소 값을 찾는다.

- max($numbers…) : 숫자 중 최대 값을 찾는다.

- random() : 0 부터 1 사이의 난수를 반환한다.

### List 함수

> 모든 List 내장 함수는 기존 List 데이터를 갱신하지 않고 새 List 데이터를 반환한다.
>
> - 모든 List 내장 함수는 Map 데이터에서도 사용할 수 있는다.

- length($list) : List의 개수를 반환한다.

- nth($list, $n) : List에서 n번째 값을 반환한다.

- set-nth($list, $n, $value) : List에서 n번째 값을 다른 값으로 변경한다.

- join($list1, $list2, [$separator]) : 두 개의 List를 하나로 결합한다.

- zip($lists…) : 여러 List들을 하나의 다차원 List로 결합한다.

- index($list, $value) : List에서 특정 값의 index를 반환한다.

### Map 함수

> 모든 Map 내장 함수는 기존 Map 데이터를 갱신하지 않고 새 Map 데이터를 반환한다.

- map-get($map, $key) : Map에서 특정 key의 value를 반환한다.

- map-merge($map1, $map2) : 두 개의 Map을 병합하여 새로운 Map를 만든다.

- map-keys($map) : Map에서 모든 key를 List로 반환한다.

- map-values($map) : Map에서 모든 value를 List로 반환한다.

### 관리(Introspection) 함수

- variable-exists(name) : 변수가 현재 범위에 존재하는지 여부를 반환한다(인수는 $없이 변수의 이름만 사용).

- unit($number) : 숫자의 단위를 반환한다.

- unitless($number) : 숫자에 단위가 있는지 여부를 반환한다.

- comparable($number1, $number2) : 두 개의 숫자가 연산 가능한지 여부를 반환한다.
