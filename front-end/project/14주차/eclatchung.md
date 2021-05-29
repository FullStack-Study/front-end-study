# 포트폴리오 사이트 만들기 - 3

## Javascript
[모듈 내보내고 가져오기](https://ko.javascript.info/import-export)
### `export` vs `export default`
1. `export`
- 변수나 함수, 클래스를 선언할 때 맨 앞에 `export`를 붙이면 내보내기가 가능해짐
```javascript
// 배열 내보내기
export let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

// 상수 내보내기
export const MODULES_BECAME_STANDARD_YEAR = 2015;

// 클래스 내보내기
export class User {
  constructor(name) {
    this.name = name;
  }
}
```
	- 클래스나 함수를 내보낼때 세미콜론은 붙이지 않는다.
- 모듈
	- 복수의 함수가 있는 라이브러리 형태의 모듈
	- 개체 하나만 선언되어있는 모듈
2. `export default`
- 해당 모듈에는 개체가 하나만 있다는 사실을 나타냄.
- default를 붙여서 모듈을 내보내면 중괄호 {} 없이 가져올 수 있음
```javascript
// 📁 main.js
import User from './user.js'; // {User}가 아닌 User로 클래스를 가져왔습니다.

new User('John');

```

## React
### 자식이 부모의 state바꾸기
- 자식이 부모의 `state`사용하기 
	- 자식의 `props`에 값을 전달하고, 자식은 `props.value` 같은 형식으로 그 값을 취하기만 하면 됨. 
- 자식이 부모의 `state`바꾸기 
	- [Change Parent Component State from Child using hooks in React | WebOmnizz](https://webomnizz.com/change-parent-component-state-from-child-using-hooks-in-react/)
```javascript
function Parent() {
    const [value, setValue] = React.useState("");

    function handleChange(newValue) {
      setValue(newValue);
    }

    // We pass a callback to Child
    return <Child value={value} onChange={handleChange} />;
}

function Child(props) {
    function handleChange(event) {
        // Here, we invoke the callback with the new value
        props.onChange(event.target.value);
    }
  
    return <input value={props.value} onChange={handleChange} />
}

```

## HTML
### div 스크롤
```CSS
.부모{
width: 80%;
height: 90vh;
color: #605D73;
background-color: rgba(245,205,208,0.7);
margin-right: 2%;
margin-top: 1.5%;
margin-bottom: 1.5%;
border-radius: 10% 10% 10% 10%;
padding: 1em;
}

.스크롤(자식){
    height: inherit;
    overflow: scroll;
    display: flex;
    flex-direction: column;
    align-content: center;
}

```
`스크롤(자식)`에 `justify-content:center;`설정을 했더니 내용 위쪽 일부가 사라지는 현상이 있었음.
#### `justify-content`
- 가로축을 기준으로 좌우에 대한 정렬을 관장함
- center :요소들을 컨테이너의 중앙으로 정렬