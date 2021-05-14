# 포트폴리오 사이트 만들기

# React
## Hook
### useEffect
- useEffect에 전달된 함수는 화면에 렌더링이 완료된 후에 수행되기 된다.
- 리액트 컴포넌트가 랜더링 될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook
- 클래스형 컴포넌트의 `componentDidMount`와 `componentDidUpdate`를 합친 형태랑 같다.
- `useEffect()`는 값이 업데이트될 때마다 실행되는데 화면에 맨 처음 렌더링 될 때만 실행하고, 업데이트될 때는 실행되지 않게 하려면 함수의 **두 번째 파라미터로 비어 있는 배열을 넣어 주면 된다**
## Ref
- 특정한 DOM 노드 혹은 컴포넌트 인스턴스에 reference를 걸어 두는 것이다.
## React-full-page


# CSS
## clip-path
- shape를 생성하는 함수를 이용하여 원하는 모양을 만들 수 있다.
- 잘린 부분은 event 리스너가 작동하지 않는다.
- [Clippy — CSS clip-path maker](https://bennettfeely.com/clippy/)

### 속성값
- `none` : 디폴트
- `url()`: SVG요소를 clip path로 지정하여 지정 대상을 클리핑한다.
- `circle()` : 원형태
- `ellipse()`
- `polygon()` : 다각형
- `inset()`

## var()
- 사용자 지정 속성
- CSS변수
- var(<custom-property-name>, <declaration-value>)
	- <custom-property-name> : 두개의 대시로 시작하는, 사용자 지정 속성의 이름을 나타내는 식별자
	- <declaration-value> : 현재 맥락에서, 주어진 사용자 지정 속성이 유효하지 않으면 대신 사용할 대체값. 새 줄, 짝 없이 닫는 괄호(), ], }) 세미콜론, 느낌표 등 특별한 의미를 가진 문자를 제외한 모든 문자를 사용할 수 있습니다.

## 마진, 보더, 패딩
- 마진 : 엘리먼트와 엘리먼트의 사이 여백
	- margin : 10px ( 전체 )
	- margin : 20px, 30px; ( 상하, 좌우)
	- margine : 20 30 10 ( 위 오른쪽 아래)
	- margine 20 30 10 20 ( 위 오른쪽 아래쪽 왼쪽)
- 테두리(보더) : 엘리먼트의 경계선
- 패딩은 테두리와 컨텐츠 사이에 있는 여백 

## a
- link : 보통의, 방문하지 않은 링크
- visited : 방문한 링크
- hover : 마우스를 올린 순간
- active : 클릭 할때의 순간
- hover는 link,visted의 뒤에 와야한다.
- active는 hover의 뒤에 와야한다.
- text-decoration:none; // 언더라인 삭제

## 뷰포트
- 화면 display 상의 표시 영역을 뜻함
- 데스크탑 뷰포트 : 브라우저 창의 뷰포트와 같음
- 모바일 뷰포트 : 창보다 크거나 작을 수 있고, 상하 좌우로 움직이거나 더블탭, 줌인, 줌아웃을 통해 뷰포트의 배율 변경가능.

# YouTube 영상 가져오기
```HTML

<iframe className="App-Personal-youtube" src="https://www.youtube.com/embed/JCwe4TmahsI?autoplay=1&mute=1&loop=1"
        title="YouTube video player" frameBorder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowFullScreen></iframe>

```

- src의 url링크의? 뒤부터 설정을 줄수 있다.
	- autoplay = 1 : 자동 재생
	- mute =1 : 무음
	- loop = 1 : 루프재생