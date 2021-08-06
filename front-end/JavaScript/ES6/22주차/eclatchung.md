  # 객체2

## 옵셔널 체이닝 ‘?.’
옵셔널 체이닝 (`optional chaining` / `?/`)을 사용하면 프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근 할 수 있음

### 옵셔널 체이닝이 중요한 이유
```javascript
let user = {}; // 주소 정보가 없는 사용자

alert(user.address.street); // TypeError: Cannot read property 'street' of undefined

//옵셔널 체이닝 생기기 이전의 방식
let user = {}; // 주소 정보가 없는 사용자

alert( user && user.address && user.address.street ); // undefined, 에러가 발생하지 않습니다.

//중첩 객체의 특정 프로퍼티에 접그하기 위해 거쳐야할 구성요소들을 AND로 연결해 실제 해당 객체나 프로퍼티가 있는지 확인하는 방법을 사용함 -> 코드가 아주 길어진다는 단점 가짐
```

### 옵셔널 체이닝의 등장
`?.` 은 `?.` 앞 평가대상이 `undefined`나 `null`이면 평가를 멈추고 `undefined`를 반환함.

```javascript

let user = {}; // 주소 정보가 없는 사용자

alert( user?.address?.street ); // undefined, 에러가 발생하지 않습니다.


let user = null;

alert( user?.address ); // undefined
alert( user?.address.street ); // undefined
```

-  user?.는 user가 `null`이거나 `undefined`인 경우에만 처리 할 수 있음
- user 값이 있을 시 -> user?.”프로퍼티이름”. -> “프로퍼티이름”이 존재해야함 아니면 에러남
- `?.`의 앞의 변수는 꼭 선언되어야함 (맨앞 / 예시의 user)
### 단락 평가
`?.`는 왼쪽 평가 대상에 값이 없으면 평가 멈춤 -> `short-circuit` (단락평가)
```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // 아무 일도 일어나지 않습니다.

alert(x); // 0, x는 증가하지 않습니다.
```

### `?.()`와 `?.[]`

```javascript
let user1 = {
  admin() {
    alert("관리자 계정입니다.");
  }
}

let user2 = {};

user1.admin?.(); // 관리자 계정입니다.
user2.admin?.(); // 평가 멈춤
```

`?.`는 읽거나 삭제는 가능하나 쓰기에서는 사용할 수 없음

## 심볼형
자바스크립트의 객체 프로퍼티 키 -> 문자형 / 심볼형

### 심볼(symbol)은 유일한 식별자를 만들고 싶을 때 사용
`Symbol()`을 사용
```javascript
let id = Symbol(); // 새로운 심볼이됨
let id = Symbol("id"); // 심볼id에는 "id"라는 설명이 붙음
```
- 유일성이 보장되는 자료형
	- 동일한 설명(심볼이름)을 가진 심볼을 여러개 만들시 각 심볼값은 다름
	- 심볼이름은 어떤 것에도 영향을 주지 않음
```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

**심볼은 문자형으로 자동 형변환되지 않는다** ⇒ 문자열로 변경 원할시 `.toString()`사용해야함

### 숨김 프로퍼티
- 심볼이용시 숨김(hidden)프로퍼티를 만들 수 있음
- 심볼은 서드파티 코드에 쩝근할 수 있음
	- 심볼 사용시 서드파티 코드 모르게 user에 식별자를 부여 할 수 있음

### 전역 심볼
- 전역 심볼 레지스트리 안에 심볼을 만들고 해당 심볼에 접근하면, 이름이 같은 경우 항상 동일한 심볼을 반환해줌
- 레지스트리 안에 있는 심볼을 읽거나 생성시에 `Symbol.for(key)` 사용하면 됨 ⇒ 이름이 key인 심볼을 반환함
```Javascript
// 전역 레지스트리에서 심볼을 읽습니다.
let id = Symbol.for("id"); // 심볼이 존재하지 않으면 새로운 심볼을 만듭니다.

// 동일한 이름을 이용해 심볼을 다시 읽습니다(좀 더 멀리 떨어진 코드에서도 가능합니다).
let idAgain = Symbol.for("id");

// 두 심볼은 같습니다.
alert( id === idAgain ); // true
```

### 시스템 심볼
- 자바스크립트 내부에서 사용되는 심볼
- 시스템 심볼 활용시 객체를 미세 조정가능

## 객체를 원시형으로 변환하기
객체의 자동 형변환
- 객체는 논리 평가시 `true`를 반환.
- 숫자형으로의 형변환은 객체끼리 빼는 연산을 할 때나 수학 관련 함수를 적용할 때 일어남.
- 문자형으로의 형 변환은 대게 객체를 출력할시에 이루어짐
### ToPrimitive
- 특수 객체 메서드를 사용시 숫자형이나 문자형으로의 형변환을 원하는 대로 조절 가능
- `hint`라는 값이 구분 기준이 됨
	- 목표로 하는 자료형
1. string
	- `alter`와 같은 문자열을 기대하는 연산 수행시 `hint`가 `string`이 됨
2. number
	- 수학 연산 적용시 `hint`는 `number`가 됨
3. default
	- 연산자가 기대하는 자료형이 확실치 않을 때 `hint`는 `default`가 됨
**모든 객체는 그냥 참으로 평가됨**

### Symbol.toPrimitive
- 자바스크립트에 `Symbol.toPrimitive`라는 내장 심볼이 존재하는데, 목표로 하는 자료형을 명명하는데 사용
```javascript
let user = {
  name: "John",
  money: 1000,

  [Symbol.toPrimitive](hint) {
    alert(`hint: ${hint}`);
    return hint == "string" ? `{name: "${this.name}"}` : this.money;
  }
};

// 데모:
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500

```
* hint가 ‘string’인 경우: toString -> valueOf 순(toString이 있다면 toString을 호출, toString이 없다면 valueOf를 호출함)
* 그 외: valueOf -> toString 순
* toString은 문자열 “[object Object]”을 반환합니다.
* valueOf는 객체 자신을 반환합니다.
### 추가 형변환
```javascript

let obj = {
  // 다른 메서드가 없으면 toString에서 모든 형 변환을 처리합니다.
  toString() {
    return "2";
  }
};

alert(obj * 2); // 4, 객체가 문자열 "2"로 바뀌고, 곱셈 연산 과정에서 문자열 "2"는 숫자 2로 변경됩니다.


let obj = {
  toString() {
    return "2";
  }
};

alert(obj + 2); // 22("2" + 2), 문자열이 반환되기 때문에 문자열끼리의 병합이 일어났습니다.
```