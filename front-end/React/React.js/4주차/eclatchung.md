# 리액트 ToDoList

## 구조
### 1. Todo Template 
	- 투두 리스트의 레이아웃을 설정하는 컴포넌트 
### 2. TodoHead
	- 오늘 날짜와 요일을 보여줌
### 3. TodoList
	- todos 배열을 내장함수 `map`을 사용하여 여러개의 TodoList컴포넌트 렌더링
### 4. TodoItem
	- 할일에 대한 컴포넌트에 대한 컴포넌트 
	- 완료 여부 toggle
	- 휴지통 기능 ⇒ 삭제 
### 5. TodoCreate
	- 새로운 할 일을 등록할 수 있게 해주는 컴포넌트 

## TodoHead
```JSX

function TodoHead() {
  const todos = useTodoState();
  const undoneTasks = todos.filter(todo => !todo.done);

  const today = new Date();
  const dateString = today.toLocaleDateString('ko-KR', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  });
  const dayName = today.toLocaleDateString('ko-KR', { weekday: 'long' });

  return (
    <TodoHeadBlock>
      <h1>{dateString}</h1>
      <div className="day">{dayName}</div>
      <div className="tasks-left">할 일 {undoneTasks.length}개 남음</div>
    </TodoHeadBlock>
  );
}

```


### `undoneTasks`
`const undoneTasks = todos.filter(todo => !todo.done);`
완료하지 않은 task의 갯수를 저장함. 

## TodoList
```JSX
function TodoList() {
  const todos = useTodoState();

  return (
    <TodoListBlock>
      {todos.map(todo => (
        <TodoItem
          key={todo.id}
          id={todo.id}
          text={todo.text}
          done={todo.done}
        />
      ))}
    </TodoListBlock>
	 );
}
```

### `todos.map`
1. `todos` : 투두 리스트 
	- todos
		- id : 투두 고유의 아이디 
		- text : 투두 리스트 내용
		- done : 완수 여부
2. `todos.map`
	- 투두 리스트의 배열을 순회
	- 순회하면서 `<TodoItem>` 를 투두 리스트 아이템 갯수 만큼 생성


## TodoItem
```JSX

function TodoItem({ id, done, text }) {
  const dispatch = useTodoDispatch();
  const onToggle = () => dispatch({ type: 'TOGGLE', id });
  const onRemove = () => dispatch({ type: 'REMOVE', id });
  return (
    <TodoItemBlock>
      <CheckCircle done={done} onClick={onToggle}>
        {done && <MdDone />}
      </CheckCircle>
      <Text done={done}>{text}</Text>
      <Remove onClick={onRemove}>
        <MdDelete />
      </Remove>
    </TodoItemBlock>
  );
}

```

### `onToggle`
	- 토글 값 변화 (완료 여부)
### `onRemove`
	- 삭제하기 
### `<MdDone>`
	- 완료시의 스타일 
### `<MdDelete>`
	- 삭제시의 스타일 