# 포트폴리오 사이트 만들기- 2

# `index.html`
## <head>
### favicon.ico
- 해당 브라우저에서 탭의 사진을 favicon이라고 한다.
- 리액트에서는 기본 `favicon.ico`라고 저장하여 사용
- 파비콘 설정
	-  `<link rel=“icon” href=“%PUBLIC_URL%/favicon.icon” />` 
- 파비콘으로 만들 사진을 `public/favicon.ico`으로 변경 안되면 확장자를 `icon`으로 실행 고고 
### title
- `eclat portfolio world`라고 탭의 홈페이지 이름 변경 가능
- `<title>elcat portfolio world</title>`


# HTML
## <div>
### 스크롤
`<div style=“overflow:scroll;”>`

### 둥글게 만들기
- `border-radius` : 1% // 전체
- `border-radius` : 상좌 상우 하좌 하우;
## <section>


# CSS
## `@font-face`
- 웹페이지의 텍스트에 온라인 폰트를 적용할 수 있다.
``` css
@font-face {
  font-family: <a-remote-font-name>;
  src: <source> [,<source>]*;
  [font-weight: <weight>];
  [font-style: <style>];
}

```

## `vh` / `vw`
- `vh` : 뷰포트의 높이값의 100분의 1의 단위
	- 브라우저 높이값이 900px일때 1vh는 9 px 
- `vw` : 뷰포트의 너비값의 100분의 1의 단위
## 투명도
- `opacity` : 배경과 글자 모두가 투명해짐
- RGBA색상을 이용하여 정해야지 투명해짐
[Hex 컬러에서 RGBA 컬러 온라인 변환 도구  - 𝗖𝗼𝗱𝗶𝗻𝗴.𝗧𝗼𝗼𝗹𝘀](https://coding.tools/kr/hex-to-rgba)