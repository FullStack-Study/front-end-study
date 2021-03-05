# 리액트


## REACT
- 사용자 인터페이스를 구축하기 위한 `선언적`이고 `효율적`이며 `유연한` `Javascript 라이브러리`이다. 
- `JSX` 라는 특수 문법을 사용하여 React 구조를 쉽게 작성한다. 
	- `javascript`의 강력한 기능을 가지고 있음
	- `JSX` 내부의 중괄호에 어떤 `javascript` 표현식도 사용가능
- `<div / >`  구문은 빌드하는 시점에서 `React.createElement(‘div’)`으로 변환됨

`변환전`
```javascript
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// 사용 예제: <ShoppingList name="Mark" />

```

`변환후`
```jsx
/*#__PURE__*/
return React.createElement("div", {
  className: "shopping-list"
}, /*#__PURE__*/React.createElement("h1", null, "Shopping List for ", props.name), /*#__PURE__*/React.createElement("ul", null, /*#__PURE__*/React.createElement("li", null, "Instagram"), /*#__PURE__*/React.createElement("li", null, "WhatsApp"), /*#__PURE__*/React.createElement("li", null, "Oculus")));
```

- Component(컴포넌트)라고 불리는 작고 고립된 코드의 파편을 이용하여 복잡한 UI를 구성함. 
	- 컴포넌트 
		- 컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 살펴 볼 수 있음. 
		- 함수 컴포넌트
``` javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
/* 
객체 인자를 받은 후 React 엘리먼트를 반환함으로 유효한 React 컴포넌트
*/
```
		- 클래스 컴포넌트 
```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
} // ES6
```

```javascript
 class Square extends React.Component { // <button> 렌더링.
     // constructor(props) { // 생성자
     //     super(props); // javascript 클래스에서 하위 클래스 생성자를 정의할때 항상 super 를 호출해야함. 생성자 가질때 super 호출 구문부터 작성해야함.
     //     this.state={
     //         value:null, //state 초기화
     //     }
     // } => 게임 상태를 유지할 필요가 없으므로 주석.

     render() {
         return (
             <button
                 className="square"
                 onClick={()=>this.props.onClick}>
                 { this.props.value }
             </button>
         );
     }
 }

```

여기서 `Square` 는 `React 컴포넌트 클래스`  또는 ` React  컴포넌트 타입`임.
	- `props` 라는 매개변수를 개별 컴포넌트는 받아옴.
		- props는 속성을 나타내는 데이터 
	- `render` 함수를 통해 표시할 뷰계층 구조를 반환함. 

#### `render` 함수
- 화면에 보고자하는 내용을 반환 (React는 설명 전달 받고 결과 표시)
- 렌더링할 내용을 경량화한 `React 엘리먼트`를 반환함.
	- 엘리먼트
		- React앱의 가장 작은 단위
		- 브라우저 DOM 엘리먼트와 달리 React 엘리먼트는 일반 객체 (plain object) 이고 쉽게 생성할 수 있음.

## `Props`
- `props`는 읽기 전용임.
- 컴포넌트는 `props`를 입력받음.
- 모든 React 컴포넌트는 자신의 `props`를 다루때 반드시 순수 함수처럼 동작해야함. 
순수 함수
```javascript
function sum(a, b) {
  return a + b;
}
//a, b는 변경 일어나지 않음
```

순수 함수X 
```javascript
function withdraw(account, amount) {
  account.total -= amount;
}
//account값 변경일어남
```

## `State`
- `state`는 `props`와 유사하지만, 비공개이며 컴포넌트에 의해 완전히 제어됨
- 
- 함수 내에 선언된 변수처럼 컴포넌트 안에서 관리가 됨
- `state`가 변경되면 컴포넌트는 리렌더링이 됨 
- `setState()`는 컴포넌트의 `state`객체에 대한 업데이트를 실행.
- `setState`호출은 비동기적으로 이루어짐.( 이벤트 핸들러 내에서 비동기적)
	- 이전 `state`값을 기준으로 값을 계산해야하면 객체 대신 `updater`함수 전달
	- 항상 `setSate`가 가장 최신의 `state`을 사용하도록 보장하기 위해서는 `setSate`에 객체 대신 함수를 전달(`updater`) ⇒ 함수 안에서 이전 `state`값을 접근할 수 있음.

### `Props` and `State`
- 리액트에서 `this.prorps`와 `this.state`는 모두 렌더링 된 값을 나타낸다. ⇒ 현재 화면에 보이는 것

## 불변성
### 데이터 변경
1. 데이터 값을 직접 변경
2. 원하는 변경 값을 가진 새로운 사본으로 데이터 교체
```javascript
1. 객체 변경

var player = {score: 1, name: 'Jeff'};
player.score = 2;
// 이제 player는 {score: 2, name: 'Jeff'}입니다.



2. 객체 변경 없이
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// 이제 player는 변하지 않았지만 newPlayer는 {score: 2, name: 'Jeff'}입니다.

// 만약 객체 spread 구문을 사용한다면 이렇게 쓸 수 있습니다.
// var newPlayer = {...player, score: 2};


```
### 기본 데이터를 변경하지 않는다면 생기는 이점
1. 불변성은 복잡한 특징들을 구현하기 쉽게 만들어준다.
2. 변화를 감지함
	- 객체가 직접적으로 수정되기 때문에 복제가 가능한 객체에서 변화를 감지하는 것은 어려움
	- 감지는 복제가 가능한 객체를 이전 사본과 비교하고 전체 객체 트리를 돌아야함.
3. React에서 다시 렌더링 하는 시기를 결정할 수 있음
	- 불변성의 가장 큰 장점은 React에서 순수 컴포넌트를 만드는 데 도움을 줌.
	- 변하지 않는 데이터는 변경이 이루어졌는지 쉽게 판단가능.
	- 컴포넌트가 다시 렌더링 할지를 결정할 수 있음.



## 함수 컴포넌트
- 더 간단하게 컴포넌트 작성
- 
### 함수에서 클래스로 변환하기
1. `React.Component`를 확장하는 동일한 이름의 `ES6 class`를 생성함
2. `render()`라고 불리는 빈 메서드를 추가함
3. 함수의 내용을 `render()` 메서드 안으로 옮김
4.  `render()`내용 안에 있는 `props`를 `this.props`로 변경함
5. 남아 있는 빈 함수 선언을 삭제함
```javascript
class Square extends React.Component { // <button> 렌더링.
     render() {
         return (
             <button
                 className="square"
                 onClick={()=>this.props.onClick}>
                 { this.props.value }
             </button>
         );
     }
 }

function Square(props) {
    return (
        <button className="square" onClick={props.onClick}>
            {props.value}
        </button>
    );
}
``` 



## 전체 소스 

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
//
// class Square extends React.Component { // <button> 렌더링.
//     // constructor(props) { // 생성자
//     //     super(props); // javascript 클래스에서 하위 클래스 생성자를 정의할때 항상 super 를 호출해야함. 생성자 가질때 super 호출 구문부터 작성해야함.
//     //     this.state={
//     //         value:null, //state 초기화
//     //     }
//     // } => 게임 상태를 유지할 필요가 없으므로 주석.
//
//     render() {
//         return (
//             <button
//                 className="square"
//                 onClick={()=>this.props.onClick}>
//                 { this.props.value }
//             </button>
//         );
//     }
// }

function Square(props) {
    return (
        <button className="square" onClick={props.onClick}>
            {props.value}
        </button>
    );
}

class Board extends React.Component { // 사각형(square)를  9개 렌더링함..
    constructor(props) {
        super(props);
        this.state = {
            squares : Array(9).fill(null), // Array.fill.null로 써서 undefined 값이 되어서 렌더링 실패하였음.
            xIsNext : true
        }
    }

    handleClick(i){
        const squares = this.state.squares.slice(); // 기존 배열을 수정하지 않고 squares 배열을 복사본을 생성하여 수정함.
        if(calculateWinner(squares) || squares[i]){
            return;
        }

        squares[i] = this.state.xIsNext ?  'X':'O';
        this.setState({
            squares : squares,
            xIsNext : !this.state.xIsNext
        })
    }

    renderSquare(i) {
        return (
            <Square
                value={this.state.squares[i]}
                onClick={() => this.handleClick(i)}
            />
        );
    }

    render() {
        const winner = calculateWinner(this.state.squares);
        let status;
        if (winner) {
            status = 'Winner: ' + winner;
        } else {
            let j ;
            for(j = 0; j < this.state.squares.length; j){
              if(!this.state.squares[j++])
                  break;
            }
            status = j == 9 ?'GAME OVER' :'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
        }
        return (
            <div>
                <div className="status">{status}</div>
                <div className="board-row">
                    {this.renderSquare(0)}
                    {this.renderSquare(1)}
                    {this.renderSquare(2)}
                </div>
                <div className="board-row">
                    {this.renderSquare(3)}
                    {this.renderSquare(4)}
                    {this.renderSquare(5)}
                </div>
                <div className="board-row">
                    {this.renderSquare(6)}
                    {this.renderSquare(7)}
                    {this.renderSquare(8)}
                </div>
            </div>
        );
    }
}

class Game extends React.Component {
    render() {
        return (
            <div className="game">
                <div className="game-board">
                    <Board />
                </div>
                <div className="game-info">
                    <div>{/* status */}</div>
                    <ol>{/* TODO */}</ol>
                </div>
            </div>
        );
    }
}

function calculateWinner(squares) {
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
    ];
    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
            return squares[a];
        }
    }
    return null;
}


// ========================================

ReactDOM.render(
    <Game />,
    document.getElementById('root')
);




```