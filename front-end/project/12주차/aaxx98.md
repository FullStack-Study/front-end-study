# 포트폴리오 1주차

# CSS

## background-image 어둡게 하기

```css
background-image: url("../img/header-img.jpg"); // 그냥 이미지

background-image: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.3)),
    url("../img/header-img.jpg"); // 어두운 이미지
```

-   backgound-image는 여러개를 겹쳐서 설정할 수 있는데, 앞쪽에 선언한 이미지가 상단으로 올라간다.
    -   linear-gradient로 검은 이미지를 만들어서 투명도를 설정하여 이미지 위에 반투명한 검은 이미지를 올린다.

## `@media` query

-   다양한 형태의 미디어 장치 마다 적합한 표현을 media query로 표현한다.
-   화면의 크기마다 레이아웃이 달라지는 반응형 웹에 사용한다.
-   미디어 유형에는 `all`, `screen`, `tv`, `printer` 등이 있다.

```css
@media [미디어유형] and (조건문) {
    css 내용
}

@media screen and (min-width: 320px) and (max-width: 768px) {
    .container {
        width: 90vw;
    }
}

```

-   미디어 유형은 `not`, `only`를 사용하여 제한할 수 있다.

    -   `not tv` : tv를 제외한 매체에 레이아웃이 적용된다.
    -   `only screen` : screen에만 레이아웃이 적용된다.
    -   생략하는 경우 기본 유형은 `all`이다.

-   `(min-width: 320px) and (max-width: 768px)` : and로 이어서 여러 조건을 추가할 수 있다.

# React

## 랜덤 색 지정하기

```js
function coloring() {
    const colors = [
        "#ffb8ce",
        "#ffc3bf",
        "#ffe26e",
        "#fffd6e",
        "#cdff8c",
        "#85ffab",
        "#abffbe",
        "#aee2e8",
        "#bdd2ff",
        "#abadff",
        "#e6c7f0",
    ];
    return colors[Math.floor(Math.random() * colors.length)];
}
```

```js
//span {disply:inline-block} 으로 설정
<span style={{ backgroundColor: coloring() }} className="tag">
    {element}
</span>
```

-   React에서 태그에 스타일을 직접 지정할 때 스타일 속성을 CamelCase로 표기한다.

# 더 해야하는 내용

-   소개말 생각해 두기
-   프로젝트 설명 추가 및 이미지 넣기
