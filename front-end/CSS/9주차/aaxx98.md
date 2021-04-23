# CSS

## 1. 의미, 정의

**Cascading Style Sheet**

-   Cascade 폭포, 종속

    -   정의 된 style이 있는지 확인하고 없으면 브라우저에서 제공하는 기본 style을 적용한다.
    -   동일한 속성 선언이 중복될 경우, 나중에 선언된 속성이 적용된다.
    -   1. Author Style
        -   `.css` style sheet을 작성하여 지정할 수 있는 stylef
    -   2. User Style
        -   웹 사이트 사용자가 지정하는 style
    -   3. Browser
        -   브라우저 상에서 제공하는 기본 style
    -   1->2->3 순으로 확인하고 적용한다.
    -   `!important`를 사용하면 우선순위와 상관 없이 무조건 적용할 수 있다. (쓰지 않는것이 좋다)

## 2. 선택자(Selectors)

HTML의 태그를 선택하는 문법

```css
/*기본적인 css 문법*/
selector {
    property: value;
}
```

-   Universal `*`
    -   모든 태그
-   type `tag`
    -   Tag의 종류 `ex) div, h1...`
-   Id `#id`
-   Class `.class`
-   State `:`
    -   `ex) button:hover` (버튼 위에 마우스를 올렸을 때 적용)
-   Attribute `[]`

    -   `ex) a[href]` (href가 있는 a tag에 적용)
    -   `ex) a[href="naver.com"]` (href="naver.com"인 a tag에 적용)
    -   `ex) a[href^="naver"]` (href가 "naver"로 시작하는 a tag에 적용)
    -   `ex) a[href$=".com"]` (href가 ".com"으로 끝나는 a tag에 적용)

### [CSS Reference](https://developer.mozilla.org/ko/docs/Web/CSS/Reference)

## 3. 레이아웃

### 3.1 display

-   display: block

    -   `div` - 기본 display: block
    -   한 줄에 한 개씩 배치됨
    -   내용(text)이 없어도 표시됨
    -   width, height을 설정 할 수 있다.

-   display: inline

    -   `span` - 기본 display: inline
    -   한 줄에 여러개 배치됨
    -   내용(text)만 표시됨
    -   width, height에 상관 없이 표시됨

-   inline-block
    -   한 줄에 여러개가 배치되는 block

## 3.2 position

-   position: static

    -   기본 설정
    -   html에 작성된 순서대로 배치하는 것
    -   left, right, top, bottom을 설정할 수 없음

-   position: relative

    -   static에서 원래 있던 위치로 부터 left, right, top, bottom 만큼 이동한 위치

-   postition: absolute

    -   바깥 box의 가장 오른쪽 위 지점을 기준으로 left, right, top, bottom 만큼 이동한 위치

-   position: fixed

    -   box에서 벗어난 페이지상에서의 위치

-   position: sticky
    -   static일 때 위치에 표시되지만, 스크롤해도 이동하지 않음

## 4. Flex Box

-   display: flex 속성을 가지는 box

-   float: text와 이미지를 배치하는 속성

    -   float: left
    -   float: center
    -   float: right

-   box 속성

    -   display
    -   flex-direction
    -   flex-wrap
    -   flex-flow
    -   justify-content
    -   align-items
    -   align-content

-   box 내부 item 속성

    -   order
        -   item 순서를 직접 지정할 때 사용
    -   flex-grow
        -   item 크기를 늘려서 inline을 꽉 차게 할 때 각 item 크기 지정에 사용
    -   flex-shrink
        -   item 크기를 줄여서 inline에 표시할 때 각 item 크기 지정에 사용
    -   flex-basis
        -   각 item이 inline에서 차지하는 크기를 %로 설정
    -   align-self
        -   item 별로 정렬방법을 다르게 할 때 사용

-   item 정렬

    -   정렬 축: main axis <-> cross axis
    -   flex-direction
        -   main axis를 결정
        -   flex-direction: row (수평 방향 정렬)
        -   flex-direction: column (수직 방향 정렬)
        -   flex-direction: row-reverse (수평 방향 역순 정렬)
        -   flex-direction: column-reverse (수직 방향 역순 정렬)
    -   flex-wrap
        -   inline item의 줄바꿈 결정
        -   flex-wrap: nowrap (기본 설정, 화면 크기가 작아져도 item 크기를 줄여 한줄에 모두 나타냄)
        -   flex-wrap: wrap(화면 크기가 줄어들면 다음 line에 나타냄)
    -   flex-flow
        -   flex-flow: [direction] [wrap]
            -   ex) `flex-flow: column nowrap`
    -   justify-content
        -   main axis에서 item 배치 방법
        -   justify-content: flex-start
            -   flex-direction: row일 때, item들을 왼쪽에 붙여서 배치
            -   flex-direction: column일 때, item들을 오른쪽에 붙여서 배치
            -   -reverse이면 반대방향으로
        -   justify-content: flex-end
            -   flex-direction: row일 때, item들을 위쪽에 붙여서 배치
            -   flex-direction: column일 때, item들을 아래쪽에 붙여서 배치
            -   -reverse이면 반대방향으로
        -   justify-content: center
            -   item들을 가운데에 배치
        -   justify-content: space-around, justify-content: space-evenly, justify-content: space-between
            -   일정 간격을 두고 item을 띄워서 배치
        -
    -   align-items

        -   align-items: baseline
            -   text를 균등한 높이로 맞춤

    -   align-content

        -   cross axis에서 item 배치 방법
        -   속성과 적용 방법은 justify-content와 동일

# Relative length units

-   px
    -   절대적인 크기를 나타내는 unit
    -   브라우저 font size 설정과는 상관 없이 font size가 그대로 유지된다.
-   em

    -   relative to parent element

    -   폰트 사이즈를 나타내는 단위, 부모 font size에 대해 상대적인 크기를 나타냄
    -   html, body에서 기본 font size는 16px

    ```html
    <div class="parent">
        Parent
        <div class="child">Child</div>
    </div>
    ```

    ```css
    .parent {
        font-size: 8em; // 16px*8 = 128px
    }
    .child {
        font-size: 0.5em; // 128px*0.5 = 64px
    }
    ```

    -   %도 부모 객체의 font size에 대해 상대적 크기를 나타낸다.

    ```css
    .parent {
        font-size: 800%; // 16px*8 = 128px
    }
    .child {
        font-size: 50%; // 128px*0.5 = 64px
    }
    ```

-   rem

    -   relative to root element
    -   root에 지정된 font size에 대해 상대적인 크기를 나타낸다.
    -   브라우저에서 지정된 font size에 rem을 곱한다.

-   vw

    -   viewport width
    -   ex) `width:50vw;` - 브라우저 width` 크기의 50% 크기로 설정한다.

-   vh

    -   viewport height
    -   ex) `height:50vh;` - 브라우저 height 크기의 50% 크기로 설정한다.

-   vmin, vmax

    -   viewport width와 viewport height 중 최소값, 최대값에 대한 상대적 크기를 나타낸다.
    -   ex) `width: 50vmin;` - 브라우저 width, height중 작은 값의 50% 크기로 설정
