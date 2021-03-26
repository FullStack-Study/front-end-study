# ReactJS로 영화 웹 서비스 만들기 - 01

페이스북에서 리액트를 만들었음

리액트 앱 실행
```shell
npm start


Local : http://localhost:3000/
On Your Network : http://~~~~~:3000/

```

1. Local  : 현재 나의 로컬환경에서의 리액트앱
2. On Your Network : 와이파이나 폰에서 테스트 하고 싶을 때 사용할 수 있는 URL


## `manifest.json`
### `PWA ( Progressive Web App) ` 
- HTTPS를 운영해야함
- 웹앱 매니페스트 `Web App Manifest`가 있어야함
- 서비스 워커를 사용해야함
- 웹과 네이티브 앱의 기능 모두 이점을 갖도록 수 많은 특정 기술과 표준 패턴을 사용해 개발된 웹앱


## React
자바스크립트로 작성해서 HTML elements 요소를 집어 넣는다. 

### `virtual DOM(Document Object Model)`
- 자바스크립트로 작성해서 HTML elements 요소를 집어 넣음
- 가상의 DOM / 실재하지 않음
- 빠름

### `component`
- HTML을 반환하는 함수
- `<App / >` 모양으로 사용 ⇒ JSX 문법
- `react application` 은 하나의 `component`만 렌더링 해야함
- 재사용이 가능함.
- `<컴포넌트이름 프로퍼티이름=value값/>`
- props.fav == { fav }

### 프로퍼티 자료형 체크
[prop-types  -  npm](https://www.npmjs.com/package/prop-types)
