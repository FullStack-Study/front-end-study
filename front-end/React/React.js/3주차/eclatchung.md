# 리액트 중간 점검


#### DOM 이란?
- 문서 객체 모델은 HTML , XML 문서의 프로그래밍 인터페이스
- DOM은 문서의 구조화된 표현을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 그들이 문서 구조, 스타일, 내용등을 변경할 수 있게 도움
- 구조화된 nodes /. roperty / method 갖고 있는 objects로 문서 표현


### react.memo ⇒ 컴포넌트 리렌더링 방지
- 컴포넌트에서 리렌더링이 필요한 상황에서만 리렌더링 하도록 설정할 수 있음


## HTML과 React의 이벤트 핸들링 
```html
//html
<button onclick="activateLasers()">
  Activate Lasers
</button>

//JSX
<button onClick={activateLasers}>
  Activate Lasers
</button>

```

- react에서는 `false`를 반환해도 기본 동작을 방지 할 수 없음
- `preventDefault`사용 해야함


```jsx
//HTML
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>


//JSX
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }
  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}

```
### `e`는 합성 이벤트 ( SyntheticEvent )
- 이벤트 핸들러는 모든 브라우저에서 이벤트를 동일하게 처리하기 위해 이벤트 래퍼 `SyntheticEvent`를 전달받음

#### 리액트 이벤트 핸드링 기초 사용법
1. onclick 말고 onClick 사용
2. 이벤트는 함수의 형태 값을 전달
3. DOM  요소에서만 이벤트 설정 가능

## src/componentes/TodoCreate.js
```jsx
//src/componentes/TodoCreate.js

function TodoCreate() {
  const [open, setOpen] = useState(false);
  const [value, setValue] = useState('');
  const dispatch = useTodoDispatch();
  const nextId = useTodoNextId();

  const onToggle = () => setOpen(!open);
  const onChange = e => setValue(e.target.value);
  const onSubmit = e => {
    e.preventDefault();
    dispatch({
      type: 'CREATE',
      todo: {
        id: nextId.current,
        text: value,
        done: false
      }
    });
    nextId.current += 1;
    setOpen(false);
    setValue('');
  };

  return (
    <>
      {open && (
        <InsertFormPositioner>
          <InsertForm onSubmit={onSubmit}>
            <Input
              autoFocus
              onChange={onChange}
              value={value}
              placeholder="할 일을 입력 후, Enter 를 누르세요"
            />
          </InsertForm>
        </InsertFormPositioner>
      )}
      <CircleButton onClick={onToggle} open={open}>
        <MdAdd />
      </CircleButton>
    </>
  );
}

```

### `useState`
- 기본적인 Hook
- 함수형 컴포넌트에서 상태를 관리해야할 일이 발생시 사용
```jsx
//배열 비구조화 할당 문법
 const [open, setOpen] = useState(false); //open과 setOpen 기본값을 false로 설정
 const [value, setValue] = useState(''); //value, setValue 기본값을 ''로 설정
```
- `useState` 호출되면 배열을 반환, 첫번째 원소는 상태값, 두번째 원소는 상태를 설정하는 함수

### `onToggle`
	- 버튼을 클릭시에 `open`이 변경이 됨
	- 토글
		- 토글이란 하나의 설정 값에서 다른 값으로 변경하는 것
		- 두가지의 상태만 존재한다.
### `onChange`
- `value` 변화가 있으면 해당 변화 `value`에 저장 
### `onSubmit`
- `dispatch`로 입력받은 값을 전달함.
- `id`값을 더함(다음 `id`값)
- `open`과 `value`값을 초기화함

## 조건부 렌더링
```JSX
 //src/componentes/TodoCreate.js
  return (
    <>
      {open && (
        <InsertFormPositioner>
          <InsertForm onSubmit={onSubmit}>
            <Input
              autoFocus
              onChange={onChange}
              value={value}
              placeholder="할 일을 입력 후, Enter 를 누르세요"
            />
          </InsertForm>
        </InsertFormPositioner>
      )}
      <CircleButton onClick={onToggle} open={open}>
        <MdAdd />
      </CircleButton>
    </>
  );

``` 

open ⇒ true일 때 입력할 수 있는 `<input>` 폼이 생성되게 `조건부 렌더링` 을 걸어둠. 

## Styled-components 
### tagged Template Literal 

```JSX
//src/componentes/TodoCreate.js

const CircleButton = styled.button`
  background: #38d9a9;
  &:hover {
    background: #63e6be;
  }
  &:active {
    background: #20c997;
  }

 /**...중간생략 **/

  transition: 0.125s all ease-in;
  ${props =>
    props.open &&
    css`
      background: #ff6b6b;
      &:hover {
        background: #ff8787;
      }
      &:active {
        background: #fa5252;
      }
      transform: translate(-50%, 50%) rotate(45deg);
    `}
`;

```

`props`의 `props.open`의 값이 `true`일때 
```css
 background: #ff6b6b;
      &:hover {
        background: #ff8787;
      }
      &:active {
        background: #fa5252;
      }
      transform: translate(-50%, 50%) rotate(45deg);
```
css으로 변경됨

⇒ 클릭전 (open전) 에는 초록색 버튼이 뜨게 하고 클릭(open)한 순간 빨간 버튼으로 변경됨.