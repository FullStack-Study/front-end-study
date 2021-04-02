# ReactJS로 영화 웹 서비스 만들기 - 02
 
## 함수형 컴포넌트 ⇒ 클래스 컴포넌트
- `state`를 사용하기 위해서 무조건 클래스 컴포넌트를 사용해야할까?
- 최근 함수형 컴포넌트에서도 `state`를 관리 할 수 있도록 진화
- 하지만 실무에서는 아직 class컴포넌트로 `state`를 관리하는게 표준..
출저
[리액트 useState() Hook : 함수형 컴포넌트로 state 관리하기](https://soldonii.tistory.com/106)

```JSX
//클래스형 컴포넌트
import React, { Component } from 'react';
import './App.css';
import Person from './Person/Person';

class App extends Component { // Component == React.Component
  state = {
    persons: [
      { name: 'Max', age: 28 },
      { name: 'Manu', age: 29 },
      { name: 'Stephanie', age: 26 }
    ],
    otherState: 'some'
  }

  switchNameHandler = () => {
    this.setState({
      persons: [
        { name: 'Max', age: 28 },
        { name: 'Manu', age: 29 },
        { name: 'hyunsol', age: 31 }
      ]
    });
  }

  render() {
    return (
      <div className="App">
        <h1>Hi, I'm a React App</h1>
        <p>This is really working!</p>
        <button onClick={this.switchNameHandler}>Switch Name</button>
        <Person name={this.state.persons[0].name} age={this.state.persons[0].age} />
        <Person name={this.state.persons[1].name} age={this.state.persons[1].age} />
        <Person name={this.state.persons[2].name} age={this.state.persons[2].age} />
      </div>
    );
  }
}


// 함수형 컴포넌트

import React, { useState } from 'react'; // Component 대신 use State
import './App.css';
import Person from './Person/Person';
const App = props => {
  const [ personsState, setPersonsState ] = useState({
    persons: [
      { name: 'Max', age: 28 },
      { name: 'Manu', age: 29 },
      { name: 'Stephanie', age: 26 }
    ],
    otherState: 'some'
  }); // useState 내부에 원래 state에 해당되는 데이터를 전달한다.

  console.log(personsState);

  const switchNameHandler = () => {
    setPersonsState({ // this.state 대신 setPersonsState
      persons: [
        { name: 'Max', age: 28 },
        { name: 'Manu', age: 29 },
        { name: 'hyunsol', age: 31 }
      ]
    });
  }

    return (
      <div className="App">
        <h1>Hi, I'm a React App</h1>
        <p>This is really working!</p>
        <button onClick={switchNameHandler}>Switch Name</button>
        <Person name={personsState.persons[0].name} age={personsState.persons[0].age} />
        <Person name={personsState.persons[1].name} age={personsState.persons[1].age} />
        <Person name={personsState.persons[2].name} age={personsState.persons[2].age} />
      </div>
    );
}

```

- ** 클래스기반 컴포넌트와 함수형 컴포넌트에서 변경된 `state` 차이점 ** 
	- 클래스 기반 컴포넌트 : 기존 state와 변경된 state는 `병합`함
	- 함수 기반 컴포넌트 : 기존 state와 변경된 state로 `대치`함


## Render()
- 리액트는 클래스 컴포넌트의 render method를 자동으로 실행함

## State
- state를 수정시에 `setState()`를 사용해야함
	- 직접적으로 `state` 변경시에  react에서 `render`를 refresh 하지 않는다.
- 매순간 내가 setState()를 호출할 때마다 react는 새로운 state와 함께 `renderfunction`을 호출함.

## 화살표 함수 / implicit return 
```javascript
//화살표 함수
let func = (arg1, arg2, ...argN) => expression
//일반적인 함수
let func = function(arg1, arg2, ...argN) {
  return expression;
};
```
1. 중괄호 없이 작성: `(…args) ⇒ expression` – 화살표 오른쪽에 표현식을 둠 ⇒ 함수는 이 표현식을 평가하고, 평가 결과를 반환
2. 중괄호와 함께 작성: `(…args) ⇒ { body }` – 본문이 여러 줄로 구성되었다면  `중괄호`를 사용해야 함. 다만, 이 경우는 `반드시 return 지시자를 사용해 반환 값을 명기`

## Life Cycle Method
![Life Cycle Image](https://cdn.filestackcontent.com/ApNH7030SAG1wAycdj3H)
- 리액트가 `component`를 생성하고 없애는 방법
- 컴포넌트가 하는것
	- `mounting` :  태어나는 것과 같음
		- constructor : javascript 문법
		- `componentDidMount`
	- `updaing` : 일반적인 업데이팅
		- cause by me! 
		- `render()`
		- `setState()` 호출 -> `component`호출→ `render`호출→ update 완료 -> `componentDidUpdate()`실행
	- `unmouting` : 컴포넌트 죽을때
		- 페이지를 바꿀때
		- state를 사용하여 component를 교체
		- 다양한 방법이 있음


## 로딩
- `componentDidMout` 사용
- data fetching을 하여서 데이터를 서버에서 받아오면 loading 완료 
