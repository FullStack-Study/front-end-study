# To do List

## 

## 리듀서 

상태 업데이트 로직을 분리한다.

```react
function todoReducer(state, action) {
  switch (action.type) {
    case 'CREATE':
      return state.concat(action.todo);
    case 'TOGGLE':
      return state.map(todo =>
        todo.id === action.id ? { ...todo, done: !todo.done } : todo
      );
    case 'REMOVE':
      return state.filter(todo => todo.id !== action.id);
    default:
      throw new Error(`Unhandled action type: ${action.type}`);
  }
}

export function TodoProvider({ children }) {
  const [state, dispatch] = useReducer(todoReducer, initialTodos);
  return children;
}
//action 의 type에 따라 어떠한 행동을 할지 설정해줌.
```

## CONTEXT

`state` 와 `dispatch` 를 Context 통하여 다른 컴포넌트에서 바로 사용 할 수 있게해주기 위함.두개의 Context에 따로따로 넣어줄 것 이러한 방식으로 구성하는 이유는 둘 중 하나의 요소만 필요한 컴포넌트에서 불필요한 렌더링을 방지 하기 위함이다.

```python
const TodoStateContext = createContext();
const TodoDispatchContext = createContext();

export function TodoProvider({ children }) {
  const [state, dispatch] = useReducer(todoReducer, initialTodos);
  return (
    <TodoStateContext.Provider value={state}>
      <TodoDispatchContext.Provider value={dispatch}>
        {children}
      </TodoDispatchContext.Provider>
    </TodoStateContext.Provider>
  );
}
```

```react
import React, { useContext } from 'react';
import { TodoStateContext, TodoDispatchContext } from '../TodoContext';

function Sample() {
  const state = useContext(TodoStateContext);
  const dispatch = useContext(TodoDispatchContext);
  return <div>Sample</div>;
}
```

이런식으로 해당 context를 사용할 수 있다.

## 커스텀 Hook 만들기

useContext를 사용하는 커스텀 hook을 만들어서 내보내자.

```react
export function useTodoState() {
  return useContext(TodoStateContext);
}

export function useTodoDispatch() {
  return useContext(TodoDispatchContext);
}
```

이런식으로 따로따로 hook을 내보낼 수 있다.

```react
import React from 'react';
import { useTodoState, useTodoDispatch } from '../TodoContext';

function Sample() {
  const state = useTodoState();
  const dispatch = useTodoDispatch();
  return <div>Sample</div>;
}
```

## Nextid값 관리하기

새로운 항목을 추가 할 때 사용할 고유id인 nextid 값을 저장하기 위한 context를 만들어주고 useRef를 사용하여 관리해주자.useRef는 컴포넌트 안에서 조회 및 수정할 수 있는 변수를 관리한다. 이것으로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링 되지 않는다.(useState와의 차이)

```react
export function TodoProvider({ children }) {
  const [state, dispatch] = useReducer(todoReducer, initialTodos);
  const nextId = useRef(5);

  return (
    <TodoStateContext.Provider value={state}>
      <TodoDispatchContext.Provider value={dispatch}>
        <TodoNextIdContext.Provider value={nextId}>
          {children}
        </TodoNextIdContext.Provider>
      </TodoDispatchContext.Provider>
    </TodoStateContext.Provider>
  );
}
```

## 커스텀 hook 에서 에러 처리

```react
export function useTodoState() {
  const context = useContext(TodoStateContext);
  if (!context) {
    throw new Error('Cannot find TodoProvider');
  }
  return context;
}

export function useTodoDispatch() {
  const context = useContext(TodoDispatchContext);
  if (!context) {
    throw new Error('Cannot find TodoProvider');
  }
  return context;
}

export function useTodoNextId() {
  const context = useContext(TodoNextIdContext);
  if (!context) {
    throw new Error('Cannot find TodoProvider');
  }
  return context;
}
```

Context 에 있는 `state` 를 받아와서 렌더링을 하고, 필요한 상황에는 특정 액션을 `dispatch` 하면된다.

## TodoList

```react
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
//상태값만 읽어온다.
```

## TodoItem 

`dispatch` ( 액션을 감지하면 작동하는 ) 을 사용해서 토글 기능과 삭제 기능을 구현해보자.

```react
function TodoItem({ id, done, text }) {
  const dispatch = useTodoDispatch();
  const onToggle = () => dispatch({ type: 'TOGGLE', id });
  const onRemove = () => dispatch({ type: 'REMOVE', id });
    //이러한식으로 액션을 확인하고 반응함
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

export default TodoItem;
```

## TodoCreate

```react
function TodoCreate() {
  const [open, setOpen] = useState(false);
  const [value, setValue] = useState('');

  const dispatch = useTodoDispatch();
  const nextId = useTodoNextId();

  const onToggle = () => setOpen(!open);
  const onChange = e => setValue(e.target.value);
  const onSubmit = e => {
    e.preventDefault(); // 새로고침 방지
    dispatch({
      type: 'CREATE',
      todo: {
        id: nextId.current,
        text: value,
        done: false
      }
    });
    setValue('');
    setOpen(false);
    nextId.current += 1;
  };
    //새로운 항목을 추가해주는 CREATE 디스패치한다.

  return (
    <>
      {open && (
        <InsertFormPositioner>
          <InsertForm onSubmit={onSubmit}>
            <Input
              autoFocus
              placeholder="할 일을 입력 후, Enter 를 누르세요"
              onChange={onChange}
              value={value}
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
//React.memo 로 감싸줌 
//리렌더링을 방지하여 리렌더링 성능 최적화를 해줄 수 있는 함수
//React.memo는 오직 props가 변경됐는지 아닌지만 체크한다
export default React.memo(TodoCreate);
```

