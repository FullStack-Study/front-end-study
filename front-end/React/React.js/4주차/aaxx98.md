# mashup-todo 2주차

## Hook

Hook은 React 16.8에 도입된 기능이다. class를 작성하지 않고도 state와 다른 React의 기능들을 사용할 수 있다.  
Hook은 함수 컴포넌트에서 React state와 생명주기 기능을 연동할 수 있게 해주는 함수이다.  
Hook은 class 안에서는 동작하지 않는다. 대신 class 없이 React를 사용할 수 있도록 해 준다.

함수 컴포넌트는 두 가지 형태로 작성할 수 있다.

```js
const Example = props => {
    // 여기서 Hook을 사용할 수 있습니다!
    return <div />;
};

function Example(props) {
    // 여기서 Hook을 사용할 수 있습니다!
    return <div />;
}
```

함수 컴포넌트는 this를 가질 수 없기 때문에(메서드로 호출해주는 객체가 없음) 클래스 컴포넌트처럼 this.state를 할당하거나 읽을 수 없다.

### 1. State Hook

```js
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0,
        };
    }

    render() {
        return (
            <div>
                <p>You clicked {this.state.count} times</p>
                <button
                    onClick={() =>
                        this.setState({ count: this.state.count + 1 })
                    }
                >
                    Click me
                </button>
            </div>
        );
    }
}
```

버튼을 클릭하면 값이 증가하는 간단한 카운터 예시이다.  
Example 컴포넌트의 state는 `{count: 0}`이고, 사용자가 버튼을 클릭하면 `this.setState()`가 호출되면서 state의 `count`가 `1` 증가한다.

```js
import React, { useState } from 'react';

function Example() {
  // 새로운 state 변수를 선언하고, 이것을 count라고 하자
  const [count, setCount] = useState(0);
```

함수 컴포넌트의 state를 관리하기 위해서 `setState`를 사용한다.  
`useState`는 인자로 초기 state 값을 받는다. 위 예시에서는 `0`을 초기값으로 설정한다.  
`setState`는 배열을 반환하는데, 첫번째 원소는 현재 상태, 두번째 원소는 Setter 함수이다. 구조분해할당에 의해 `count`에는 현재상태 0, `setCount`에는 count의 Setter 함수가 할당된다.

```js
import React, { useState } from "react";

function Example() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    );
}
```

### 2. Effect Hook

Effect Hook을 사용하면 함수 컴포넌트에서 **side effect**를 수행 할 수 있다.

-   데이터 가져오기
-   state에 대한 구독(subscription) 설정하기
-   수동으로 리액트 컴포넌트의 DOM 수정하기

다음과 같은 항목들이 side effect가 된다.

클래스 컴포넌트의 생명주기 메서드의 역할을 `useEffect`가 한다.

-   생명주기 메서드
    -   컴포넌트의 각 단계에서 실행되는 커스텀 기능이다.
    -   mounting: 컴포넌트가 만들어지고 DOM에 삽입될 때
        `componentDidMount`
    -   update: 컴포넌트가 업데이트 될 때(특정 props가 바뀔 때)
        `componentDidUpdate`
    -   unmounted: 컴포넌트가 DOM에서 제거될 때
        `componentWillUnmount`

side effect는 리액트가 DOM을 업데이트 한 이후 발생한다.

위 카운터 예시에서, 클릭 횟수가 변하면 제목에 클릭한 횟수가 반영되도록 해보자.

```js
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0,
        };
    }

    componentDidMount() {
        document.title = `You clicked ${this.state.count} times`;
    }
    componentDidUpdate() {
        document.title = `You clicked ${this.state.count} times`;
    }

    render() {
        return (
            <div>
                <p>You clicked {this.state.count} times</p>
                <button
                    onClick={() =>
                        this.setState({ count: this.state.count + 1 })
                    }
                >
                    Click me
                </button>
            </div>
        );
    }
}
```

위 코드는 클래스 컴포넌트의 예시이다. 컴포넌트가 마운트 된 직후와 업데이트 될 때 하는일(side effect)가 같고, 내부 코드도 중복되고 있다.  
개념적으로 렌더링 이후에 같은 코드가 실행되도록 설계한 것이다.

함수 컴포넌트로 바꿔보자.

```js
import React, { useState, useEffect } from "react";

function Example() {
    const [count, setCount] = useState(0);

    // componentDidMount, componentDidUpdate와 같은 방식으로
    useEffect(() => {
        // 브라우저 API를 이용하여 문서 타이틀을 업데이트
        document.title = `You clicked ${count} times`;
    });

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    );
}
```

`useEffect`를 통해 컴포넌트가 렌더링 이후 해야할 일을 설정 할 수 있다.

매개변수로 함수를 넘기고 있는데, 이 함수를 effect라고 한다. effect를 기억했다가 DOM 업데이트를 수행하고 난 후(렌더링 후), effect를 호출한다.

`useEffect`는 컴포넌트 안에서 호출하므로, 특별한 API 없이도 state 변수나 어떤 prop에도 접근할 수 있게 된다.

앞선 에시는 unmounted가 포합되지 않았지만, 컴포넌트의 마운트를 해제하려면 컴포넌트를 subscribe 하고있어야 한다.

```js
class FriendStatus extends React.Component {
    constructor(props) {
        super(props);
        this.state = { isOnline: null };
        this.handleStatusChange = this.handleStatusChange.bind(this);
    }

    componentDidMount() {
        ChatAPI.subscribeToFriendStatus(
            this.props.friend.id,
            this.handleStatusChange
        );
    }
    componentWillUnmount() {
        ChatAPI.unsubscribeFromFriendStatus(
            this.props.friend.id,
            this.handleStatusChange
        );
    }
    handleStatusChange(status) {
        this.setState({
            isOnline: status.isOnline,
        });
    }

    render() {
        if (this.state.isOnline === null) {
            return "Loading...";
        }
        return this.state.isOnline ? "Online" : "Offline";
    }
}
```

```js
import React, { useState, useEffect } from "react";

function FriendStatus(props) {
    const [isOnline, setIsOnline] = useState(null);

    useEffect(() => {
        function handleStatusChange(status) {
            setIsOnline(status.isOnline);
        }
        ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
        // effect 이후에 어떻게 정리(clean-up)할 것인지 표시합니다.
        return function cleanup() {
            ChatAPI.unsubscribeFromFriendStatus(
                props.friend.id,
                handleStatusChange
            );
        };
    });

    if (isOnline === null) {
        return "Loading...";
    }
    return isOnline ? "Online" : "Offline";
}
```

`useEffect`에서 return하는 함수는 컴포넌트의 마운트가 해제될 때 실행된다.  
`useEffect`가 return 하는 함수를 `cleanup 함수`라고 한다.

### userReducer

```js
const [state, dispatch] = useReducer(reducer, initialState);
```

-   매개변수 `reducer`:
    현재 상태와 액션 객체를 파라미터로 받아와서 새로운 상태를 반환해 주는 함수
-   매개변수 `initialState`: 초기 상태

`useReduce()`를 사용하면 `state`는 현재 컴포넌트의 상태가 되고, `dispatch`는 action을 발생시키는 함수가 된다.

```js
import React, { useReducer } from "react";

function reducer(state, action) {
    switch (action.type) {
        case "INCREMENT":
            return state + 1;
        case "DECREMENT":
            return state - 1;
        default:
            return state;
    }
}

function Counter() {
    const [number, dispatch] = useReducer(reducer, 0);

    const onIncrease = () => {
        dispatch({ type: "INCREMENT" });
    };

    const onDecrease = () => {
        dispatch({ type: "DECREMENT" });
    };

    return (
        <div>
            <h1>{number}</h1>
            <button onClick={onIncrease}>+1</button>
            <button onClick={onDecrease}>-1</button>
        </div>
    );
}

export default Counter;
```

## Context

context를 이용하면 단계마다 일일이 props를 넘겨주지 않고도 컴포넌트 트리 전체에 데이터를 제공할 수 있다.

-   Context 생성

    다음과 같이 Context 객체를 생성할 수 있다.

    ```js
    const MyContext = React.createContext(defaultValue);
    ```

    -   `defaultValue`는 적절한 Provider를 찾지 못했을 때만 사용되는 값이다.

-   Context.Provider

    ```js
    <MyContext.Provider value={/* 어떤 값 */}>
    ```

    Provider는 context를 구독하는 컴포넌트들에게 context의 변화를 알리는 역할을 한다.  
    `value` prop을 받아서 이 값을 하위 컴포넌트에게 전달한다.

    Provider 하위의 컴포넌트들은 context를 구독하는 컴포넌트들이다. Provider의 `value ` prop가 바뀔 때 마다 다시 렌더링 된다.

-   `useContext()`

    context 객체를 받아 그 context의 현재 값을 반환한다.

    ```js
    const value = useContext(MyContext);
    ```
