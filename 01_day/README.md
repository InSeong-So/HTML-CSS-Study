# 1일차

## 개요

- HTML(Hyper Text Markup Language)

  - 페이지에 제목, 문단, 표 등을 정의하고 구조와 의미를 부여하는 정적 언어
  - 웹 구조 담당
  - 온전히 튼튼한 구조(Semantic)를 만드는데 사용한다.

- CSS(Cascading Style Sheets)

  - 마크업 언어(HTML, XML 등)가 실제 표시되는 방법(색상, 크기, 폰트, 레이아웃 등)을 지정하여 콘텐츠 구조를 꾸며주는 정적 언어
  - 웹의 시각적 표현 담당

## 웹 표준(Web Standard)

> 웹에서 사용되는 표준 기술이나 규칙을 의미하며 W3C의 권고안에 나온 기술들이 여기에 해당된다.

- 웹 표준으로 웹 브라우저들이 만들어진다.
  - `표준 기술을 해석하는 차이`와 `새로운 기술 삽입(표준화 제정 단계에 따른)` 등으로 여러 브라우저가 생겼다.
- ActiveX, Flash 같은 기술은 표준이 아니다.
- 대부분 표준화 제정 단계의 권고안(REC)에 해당하는 기술이 표준이다.

## 크로스 브라우징(Cross Browsing)

> 여러 브라우저에서 동일한 사용자 경험(같은 화면, 같은 동작)을 줄 수 있도록 제작하는 기술, 방법 등을 일컬음

- 보통 MSIE 브라우저는 웹 표준을 준수하지 않았으므로 대부분 IE에 문제가 없으면 다른 브라우저도 이상이 없다.

## 웹 접근성

> 정상적인 웹 콘텐츠 사용이 가능한 일반 사용자부터 고령자, 장애인 같은 신체적, 환경적 조건에 제한이 있는 사용자를 포함해 모든 사용자들이 접근할 수 있는 웹 콘텐츠를 제작하는 방법

- 청각 장애인을 위해 영상에 자막을 넣는 것
- 마우스를 사용할 수 없는 사람들을 위해 키보드를 통해서도 웹을 이용할 수 있게 하는 것(혹은 그 반대)
- 이미지에 대체 텍스트를 제공하는 간단한 방법들
- 참조 : `정보 통신 보조기기`, `웹 접근성 품질인증 마크`

## 비트맵과 벡터 이미지

- 비트맵(Bitmap) : 각 픽셀이 모여 만들어진 정보의 집합, 레스터(Raster) 이미지라고도 부름
  - 픽셀 단위로 화면에 렌더링(컴퓨터가 화면에 그림을 그리는 것)
  - 일반적으로 사용하는 대부분의 이미지가 비트맵 형식이며 그림판, 포토샵 같은 툴로 편집이 가능
  - 정교하고 다양한 색상을 자연스럽게 표현 || 확대/축소 시 계단 현상, 품질 저하
- 벡터(Vector) : 수학적 정보의 형태(Shape)들이 만들어내는 결과물
  - 이미지가 가지고 있는 점, 선, 면의 위치(좌표), 색상 등의 정보를 온전히 가지고 있으며 그를 화면에 렌더링한다.
  - 좀 더 많은 연산을 해야 하지만 해상도(픽셀)로부터 자유롭게 렌더링할 수 있다.
  - 수학적 정보만을 가지고 있기 때문에 확대, 축소를 해도 이미지가 깨지지 않고 용량도 변화하지 않는다.
  - 일러스트 툴로 편집이 가능하다.
  - 확대/축소에서 자유롭고 용량 변화가 없음 || 정교한 이미지(인물, 풍경 사진 등)를 표현하기 어려움

## JPG(JPEG, Joint Photographic coding Experts Group)

- Full-color와 Gray-scale의 압축을 위해 만들어졌으며 압축률이 훌륭해 사진/예술 분야에서 많이 사용된다.
- 손실 압축(높은 압축률을 가졌는데도 적은 용량이다)
- 표현 색상도(24비트, 약 1600만 색상)가 뛰어나 고해상도 표시장치에 적합
- 이미지의 품질과 용량을 쉽게 조절 가능
- 가장 널리 쓰이는 이미지 포맷

## PNG(Portable Network Graphics)

- Gif의 대체 포맷
- 비손실 압축
- 8비트(256 색상) / 24비트(약 1600만 색상) 컬러 이미지 처리
- Alpha Channer 지원(투명도)
- W3C 권장 포맷

## GIF(Graphics Interchange Format)

- 이미지 파일 내에 이미지 및 문자열 같은 정보들을 젖아할 수 있다.
- 여러 장의 이미지를 한 개의 파일에 담을 수 있다(움직이는 이미지).
- 8비트 컬러만 지원(다양한 색상을 표현하는 작업에는 적합하지 않음)

## WEBP

- JPG, PNG, GIF를 모두 대체할 수 있는 구글이 개발한 이미지 포맷
- 완벽한 손실/비손실 압축 지원
- GIF 같은 애니메이션 지원
- Alpha Channel(손실, 비손실 모두)
- 지원 브라우저가 한정적이다

## SVG(Scalable Vector Graphics)

- 마크업 언어 기반의 벡터 그래픽을 표현하는 포맷
- 해상도의 영향에서 자유로움
- CSS로 Styling 가능
- JavaScript EventHandling 가능
- 코드 혹은 파일로 사용 가능

## 특수기호

| 기호 | 영어(발음)                               | 한글           |
| ---- | ---------------------------------------- | -------------- |
| `    | Grave(그레이브)                          | -              |
| ~    | Tilde(틸드)                              | 물결표시       |
| !    | Exclamation(엑스클러메이션) mark         | 느낌표         |
| @    | At(엣) sign                              | 골뱅이         |
| #    | Number(넘버) sign, Sharp(샵)             | 샵, 우물 정    |
| $    | Dollar(달러) sign                        | 달러           |
| %    | Percent(퍼센트) sign                     | 퍼센트         |
| ^    | Caret(캐럿)                              | -              |
| &    | Ampersand(엠퍼센드)                      | -              |
| \*   | Asterisk(에스터리스크)                   | 별표           |
| -    | Hyphen(하이픈), Dash(대쉬) 마이너스      |
| \_   | Underscore(언더스코어), Low dash(로대쉬) | 밑줄           |
| =    | Equals(이퀄) sign                        | 이꼬르         |
| “    | Quotation(쿼테이션) mark                 | 큰 따옴표      |
| ‘    | Apostrophe(아포스트로피)                 | 작은 따옴표    |
| :    | Colon(콜론)                              | 땡땡이         |
| ;    | Semicolon(세미콜론)                      | 털 달린 땡땡이 |
| ,    | Comma(콤마)                              | 쉼표           |
| .    | Period(피리어드), Dot(닷)                | 점, 마침표     |
| ?    | Question(퀘스천) mark                    | 물음표         |
| /    | Slash(슬래쉬)                            | -              |
|      | Vertical bar(버티컬 바)                  | -              |
| \    | Backslash(백슬래쉬)                      | -              |
| ()   | Parenthesis(퍼렌서시스)                  | (소)괄호       |
| {}   | Brace(브레이스)                          | 중괄호         |
| []   | Bracket(브래킷)                          | 대괄호         |
| <>   | Angle Bracket(앵글 브래킷)               | 꺽쇠괄호       |

- [HTML Entity List](https://www.freeformatter.com/html-entities.html)

## HTML 기본 문법

- 태그
    > 열리고 닫히는 한 쌍의 구조를 가지고 있다.
    > - open tag, close tag

    ```html
    <tag></tag>
    <tag>CONTENT</tag>
    ```
    ```html
    <h1>h1태그:주제</h1>
    <p>p태그:본문</p>
    ```

- 속성(Attribute)과 값(Value)

    ```html
    <tag 속성="값"></tag>
    ```
    ```html
    <!-- 닫히는 태그가 없으면 빈 태그(Empty tag)라고 부른다. -->
    <img src="./photo.jpg" alt="사진" />    <!-- alt: alternative, 대체 텍스트 -->
    <div class="name">홍길동</div>          <!-- div: division, 분할 -->
    ```

- 부모와 자식 요소
    > 태그 A가 태그 B의 콘텐츠로 사용되면 태그 B는 태그 A의 부모 요소, 태그 A는 태그 B의 자식 요소라고 한다.
    > - 부모 요소의 부모 요소를 조상, 상위 요소 등으로 부른다.
    > - 자식 요소의 자식 요소를 후손, 하위 요소 등으로 부른다.
    
    ```html
    <parent>
        <child></child>
    </parent>
    ```

- 빈 태그
    > HTML에서 닫히는 개념이 없는 태그
    ```html
    <!-- '/'가 없는 빈 태그 -->
    <tag>

    <!-- '/'가 있는 빈 태그 -->
    <tag />
    ```

## HTML 문서의 범위
- HTML : HTML 문서의 범위를 나타내는 태그
    - HTML 문서의 전체 범위를 정의
    - 웹 브라우저가 해석해야 할 HTML 문서가 어디에서 시작하며, 어디에서 끝나는지 알려준다.

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <!-- 문서의 정보 -->
        </head>
        <body>
            <!-- 문서의 구조 -->
        </body>
    </html>
    ```

- HEAD : HTML 문서의 정보 범위를 나타내는 태그
    - 웹 브라우저가 해석해야 할 HTML 문서의 정보 범위를 정의
    - 여기서 말하는 정보에는 웹 페이지의 제목, 웹 페이지의 문자 인코딩 방식, 연결할 외부 파일의 위치, 웹 페이지를 구조화하기 위한 기본 세팅 값 같은 것들을 말한다.
    - 다르게는 ‘화면을 구성하기 위한 기본 설정’이라고 표현할 수 있다.

    ```html
    <head>
        <!-- title : HTML 문서의 제목을 정의하며 웹 브라우저의 탭에 표시 -->
        <title>네이버<title>
        <!-- meta : HTML 문서에 관한 정보(표시 방식, 제작자(소유자), 내용, 키워드 등) -->
        <!--      : 검색 엔진 또는 브라우저에 제공하며 빈 태그(Empty tag)이다. -->
        <meta charset="UTF-8"></meta>
        <!-- -link : 외부 문서를 연결할 때 사용 -->
        <link rel="stylesheet" href="./css/main.css">
    <head>
    ```

- BODY : HTML 문서의 구조 범위를 나타내는 태그
    - 웹 브라우저가 해석해야 할 HTML 문서의 구조 범위를 정의
    - 구조는 사용자가 화면을 통해서 볼 수 있는 내용(콘텐츠)의 형태나 레이아웃 등을 의미하며 로고, 헤더, 푸터, 내비게이션, 메뉴, 버튼, 입력창, 팝업, 광고 등 보이는 모든 것들이 구조에 해당된다.
    - 구조는 BODY 범위 안에서만 생성한다.

    ```html
    <div>
        'div'는 'division'의 약자로 분할을 뜻하며 문서의 부분이나 섹션을 정의한다.
        단순히 특정 범위를 묶는(wrap) 용도로 많이 활용한다.
    </div>

    <img />
    HTML에 이미지를 삽입할 때 사용한다.
    HTML의 img 태그와 CSS 속성에서 이미지를 삽입하는 방법 두가지가 있다.
    src, alt 속성 두 가지를 반드시 정의해야 한다(웹 표준).
    ```

- DOCTYPE(DTD, Document Type Definition)
    ```html
    <!-- HTML 5 -->
    <!DOCTYPE html>

    <!-- XHTML 1.0 Transitional -->
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    ```
  - 마크업 언어에서 문서의 형식을 정의
  - 웹 브라우저에서 우리가 제공할 HTML 문서를 어떤 HTML 버전의 해석 방식으로 구조화하면 되는지를 알려준다.