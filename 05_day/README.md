# 5일차

- display 수정 : `float` 속성이 추가된 요소는 `display` 속성의 값이 대부분 `block`으로 수정됨

    |지정값|변화값|
    |------|------|
    |inline|block|
    |inline-block|block|
    |inline-table|block|
    |table-row|block|
    |table-row-group|block|
    |table-column|block|
    |table-column-group|block|
    |table-cell|block|
    |table-caption|block|
    |table-header-group|block|
    |table-footer-group|block|
    |flex|flex / float속성 효과없음|
    |inline-flex|inline-flex / float속성 효과없음|
    |그외|변화없음|

    ```css
    a,
    span {
    width: 100px;
    height: 100px;
    background: red;
    float: left;
    }
    ```
    ```html
    <a href="#"></a>
    <span></span>
    ```
    - `<a>, <span>` 요소는 대표적인 inline요소로 가로/세로 너비를 가질 수 없지만 float 속성이 있을 경우 가로/세로 너비를 사용할 수 있다.

### clear
> `float` 속성이 적용되지 않도록 지정(해제)

|값|의미|기본값|
|--|----|------|
|none|요소 띄움 허용|none|
|left|왼쪽 띄움 해제|	|
|right|오른쪽 띄움 해제|	|
|both|양쪽(왼쪽, 오른쪽) 모두 띄움 해제|

### position
> 요소의 위치 지정 방법의 유형(기준)을 설정

|값|의미|기본값|
|--|----|------|
|static|유형(기준) 없음 / 배치 불가능|static|
|relative|요소 자신을 기준으로 배치||
|absolute|위치 상 부모 요소를 기준으로 배치||
|fixed|브라우저(뷰포트)를 기준으로 배치||
|sticky|스크롤 영역 기준으로 배치||

- relative : 요소 자신을 기준으로 배치
    ```css
    /* 배치의 용도로 활용하는 걸 권장하지 않는다. */
    .box {
    position: relative; /* 기준 + 배치 */
    top: 50px;
    right: 100px;
    }
    ```

- absolute : 위치 상 조상 요소를 기준으로 배치
  - 위치 상 부모 요소에 static을 제외한 position속성의 값이 반드시 존재해야 한다.
  - 위치 상 부모 요소에 미리 적용된 position속성의 값이 없는 경우, relative 값을 적용한다.

    ```html
    <div class="parent-box">
    <div class="child-box"></div>
    </div>
    ```
    ```css
    .parent-box {
    position: relative; /* 기준 */
    }
    .child-box {
    position: absolute; /* 배치 */
    top: 50px;
    right: 100px;
    }
    ```

  - 부모 요소에 position속성의 값이 없다면 조상(상위)요소로 올라가면서 위치 상 부모 요소를 찾아 기준한다.

      ```html
      <div class="grand-box">
      <div class="parent-box">
          <div class="child-box"></div>
      </div>
      </div>
      ```
      ```css
      .grand-box {
      position: relative; /* 기준 */
      }
      .parent-box {
      /* 기준 아님 */
      }
      .child-box {
      position: absolute; /* 배치 */
      top: 50px;
      right: 100px;
      }
      ```