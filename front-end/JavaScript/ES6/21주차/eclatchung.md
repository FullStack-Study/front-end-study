# 객체

## 객체 (기본) 

### 자료형
#### 원시형 (Primitive Type)
1. 숫자형
2. bigint
3. 문자형
4. 불린형
5. null
6. undefined : 할당되지 않은 값
7. 심볼형 : 객체의 고유 식별자를 만들때 사용

#### 객체형
- 다양한 데이터를 담을 수 있음
- 키로 구분된 데이터 집합이나, 복잡한 개체 저장
- {…} 이용
	- 중괄호안
		- `key : 값`로 구성된 프로퍼티 여러개를 넣을 수 있음
		- key : 문자형 / 프로퍼티 이름, 식별자
		- 값 : 모든 자료형

### 객체 생성 ( 빈객체 )
```Javascript
let user = new Object(); //  객체 생성자 문법
let user = {}; // 객체 리터럴 문법
```

### 객체 프로퍼티 삽입
```javascript
let user = {
	name : "Yun",
	age : 25, //마지막의 , 는 trailing/hanging쉼표라고 하고 모든 프로퍼티가 유사한 형태가 되어 프로퍼티 작성코드를 수정하는데 쉬워진다.
};

user.isAdmin = true; // user와 isAdmin사이의 .은 점표기법 (dot notation)

//여러 단어를 이용한 프로퍼티 이름
let user1 ={
	..
	"likes birds" : true, // 따옴표를 붙여야함
	..
};
```
**상수 객체는 수정이 될수 있다**
```javascript
const user ={name : "si"};
user.name = "yun"; // 가능
```

### 프로퍼티 삭제
```javascript
delete user.name;
```

### 대괄호 표기법 (square bracket notation)
```javascript
let user = {
	"likes birds":true,
}; 
//1. 
console.log(user["likes birds"]);

//2. 
let key = "likes birds";

console.log(user[key]);

// 1과 2는 동일함
```

### 계산된 프로퍼티 (computed property)
```javascript
let fruit = promt("~~","apple");

let bag = {
	[fruit] : 5, // 변수 fruit를 사용하여 프로퍼티 이름을 동적으로 사용
	[fruit + "isFavorite"] : true, // fruit의 내용 +. sFavorite  ==> if(fruit == "apple"){ appleisFavorite }
};
```

### 단축 프로퍼티
```javascript
//1
function makeUser1(name, age){
	return {
		name : name,
		age : age,
	};
}
//2
function makeUser2(name, age){
	return {
		name, // name : name 과 같음
		age,
		}
	}
```
### 프로퍼티 이름의 제약사항
- 객체 프로퍼티키에 쓸 수 있는 문자열에는 제약이 없음
- 단, `__proto__`만 특별대우
	- `__proto__` : 자바스크립트의 객체는 명세서에서 명명한 `[[prototype]]`이라는 숨김 프로퍼티를 갖음
	- `null`값이나 다른 객체에 대한 참조가 됨
### in 연산자로 프로퍼티 존재 여부 확인
- javascript는 존재하지 않는 프로퍼티에 접근시 에러 발생하지 않고 `undefined` 변환함
그래서 프로퍼티 존재 여부를 undefined을 이용해서 알수 있음
```javascript
let user = {};

if(user.isExist === undefined){
	//실행됨
};
```
undefiend말고 프로퍼티 여부를 확인 할수 있는 연산자. ⇒ `in`연산자 
`프로퍼티이름 in object`
```javascript
let user = { age : 25};
console.log("age" in user); // true;
console.log("name" in user); // false; 

let keyName = "age"
console.log(keName in user) // true;
```
- `in`프로퍼티 왼쪽은 반드시 프로퍼티 이름이여야함
- 프로퍼티 존재여부를 `in 프로퍼티`를 사용하는 이유는 임의로 프로퍼티값을 `undefined`값으로 주면  `===undefined`연산에서 미스 (놓치는 경우)가 생기기 때문이다.
### for … in 반복문
- 객체의 모든 키를 순회
```Javascript
for(key in object){
 // key를 이용하여 object body를 실행
}

let user = {name : "Yun", age : 25};

for(key in user){
	console.log(key); // name, age
	console.log(user[key]); // Yun, 25
};
```
### 객체 정렬방식
- 특별하다
	- 정수 프로퍼티 (선언은 문자열로 해야함)는 자동정렬되고 그외는 객체에 추가한 순서로 정렬한다.

## 참조에 의한 객체 복사
**원시 타입과 객체타입의 근본적인 차이** ⇒ 객체는 **참조(by reference)에 의해** 저장되고 복사됨

- 객체 ⇒ 변수에 객체 그대로 저장되는 것이 아닌, 객체가 저장되어 있는 **메모리 주소**에 대한 **참조값**이 저장됨
```javascript
let user = {name : "Yun"};
let admin = user;

console.log(admin.name); // "Yun"

admin.name = "yunny";
console.log(user.name); // "yunny";

user.age = 25;
consolel.log(admin.age); //25
```

### 참조에 의한 빈교
객체 비교 시, 동등 연산자 == 와 일치 연산자 ===는 동일하게 동작함
```javascript
let a = {};
let b = a;
 console.log(a == b); // true;
console.log(a === b); // true;

let c ={};

console.log(a ==c ) // false;
console.log(a ===c ) //false;
```
- obj1 > obj2 같은 대소 비교나 obj == 5같은 원시값과의 비교에선 객체가 원시형으로 변환
### 객체 복제와 Object.assign()
- 복제 : 객체의 값은 똑같으면서 서로 독립적인 객체 만들기
- javascript는 객체 복제 내장 메서드를 지원하지 않아 어려움
- for .. in 을 써서 프로퍼티를 순회하여 원시 수준까지 프로퍼티복사 하면됨
- Object.assign을 이용해서 복사하면됨
	- `Obejct.assign(dest, [src1, src2…..,srcn])`
		- dest : 목표로 하는 객체
		- [src1,…,srcn] : 복사하고자 하는 객체
		- [src1,…,srcn] 의 프로퍼티를 dest에 복사하고 dest 반환

### 중첩 객체 복사
- 중첩 객체
```javascript
let user = {
	name : "Yun",
	sizes : {
		heights : 163,
	}
};

```
- 위의 중첩객체를 바로 Object.assgin을 쓰면 user의 하위 객체인 sizes는 복제될 객체와 같은 sizes를 공유함.
	- user[key]의 각값을 검사하면서 그값이 객체인 경우, 객체의 구조도 복사해주는 반복문 사용해야함 ⇒ 깊은 복사(복제) (deep cloning)
	- lodash의 _.cloneDeep(obj)이용

## 가비지 컬렉션
- 자바스크립트는 도달 가능성이라는 개념을 사용해 메모리 관리를 수행함.
- 도달 가능한 (reachable)
	- 어떻게든 접근하거나 사용할 수 있는 값 
	 - 도달 가능한 값은 메모리에서 삭제되지 않는다.
- 태생부터 도달 가능한 값 == 루트
	- 현재 함수의 지역변수오 매개 변수
	- 중첩 함수의 체인에 있는 함수에서 사용되는 변수와 매개변수
	- 전역 변수 
	- 등
- 루트가 참조하는 값이나 체이닝으로 루트에서 참조할 수 있는 값은 도달 가능한 값이 됨.
```javascript
let user = {	name : "John"}; // 1

user = null; // 1의 {name : "John"} 객체는 해당 라인으로 인해 도달 가능한 상태가 아님. 가비지 컬렉터에서 해당 객체에 저장된 데이터를 삭제하고 해당 객체를 메모리에서 삭제함
```

### 내부 알고리즘 ( mark and sweep)
1. 가비지 컬렉터는 루트 정보를 수집하고 이를 기억 (mark)한다.
2. 루트가 참조하고 있는 모든 객체를 방문하고 이것들을 mark함
3. mark된 모든 객체에 방문하고 그 객체들이 참조하는 객체도 mark함. 한번 방문한 객체는 다 mark해서 같은 객체를 다시 방문하지 않음
4. 루트에서 도달 가능한 모든 객체를 방문할 때까지 위 과정을 방문
5. mark되지 않은 모든 객체 메모리에서 삭제
- 최적화 기법
	- generational collection : 세대별 수집
	- incremental collection : 점진적 수집
	- idle-time collection : 유휴 시간 수집

## 메서드와 this
객체 프로퍼티에 할당된 함수를 메서드라고 함
```javascript
let user = {name : "Yun", age : 25};

function sayHi(){ return console.log("Hi");};
user.sayHi = sayHi;

user.sayHi(); // "Hi";
```

### 메서드 단축 구문
```javascript
//1
user = {
	sayHi : function(){}
}
//2
user = {
	sayHi(){
	}
};
```
- `1`과 `2` 는 동일함

### 메소드와 this
- 메소드는 객체에 저장된 정보에 접근할 수 있어야 제 역할을 할 수 있음
- 메서드 내부에서 `this` 키워드를 사용하면 객체에 접근 할 수 있음
- 점앞의 `this`는 객체를 나타냄, 메서드를 호출 할 때 사용된 객체

### 자유로운 this
- this값은 런타임에 결정됨. (컨텍스트에 따라 달라짐)
- 메서드가 어디서 정의되었는지에 상관없이 this는 점앞의 객체가 무엇인지에 따라 자유롭게 결정

### 객체 없이 호출하기 `this===undefined`
```javascript
function sayHi() {
  alert(this);
}

sayHi(); // undefined
```
- 엄격모드일땐 `undefined`
- 엄격모드가 아닐 때 `전역 객체` 참조
- 브라우저 환경에선 `window 전역객체` 참조

### this가 없는 화살표 함수
- 화살표함수는 일반함수와 달리 ‘고유한’ this 가지지 않음
- 화살표 함수에서 this참조시 화살표 함수가 아닌 평범한 외부 함수에서 this가져옴
- 별개의 this가 만들어지는 것을 원치 않고 외부컨텍스트에 있는 this를 이용하고 싶은 경우 화살표 함수가 유
```javascript
let user = {
  firstName: “보라”,
  sayHi() {
    let arrow = () ⇒ alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
```

## new 연산자와 생성자 함수
- 객체 리터럴 {…}를 사용하면 객체를 쉽게 만들 수 있음
- `new`연산자와 생성자 함수를 사용하면 유사한 객체 여러개를 쉽게 만들 수 있음
 - 생성자 함수 (constructor function)
	1. 함수 이름의 첫글자는 대문자로 시작
	2. 반드시 new 연산자를 붙여 실행
```javascript
functino User(name){
	this.name = name;
	this.isAdmin = false;
};

let user = new User("보라");
```
#### 실행순서
1. 빈 객체를 만들어 this에 할당
2. 함수 본문 실행. this에 새로운 프로퍼티 추가해 this 수정
3. this 반환
- 생성자의 의의 ⇒ 재사용 할 수 있는 객체 생성 코드를 구현
- 모든 함수는 생성자 함수가 될 수 있음
### new.target과 생성자 함수
- new.target 프로퍼티를 사용하면 함수가 new 와 함께 호출 되었는지 아닌지 알 수 있음
- 일반적인 방법으로 함수 호출 ⇒ undefined 반환
- new와 함께 함수 호출 ⇒ 함수 자체를 반환 
### 생성자와 return 문
- 생성자 함수엔 보통 return 문이 없음
- return 존재시
	- 객체를 return 한다면 this대신 객체 반환
	- 원시형을 return 한다면 return문이 무시됨
### 생성자내 메서드
- 생성자 함수를 활용하면 매개변수를 이용해 객체 내부를 자유롭게 구성할 수 있음
```javascript
function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert( "제 이름은 " + this.name + "입니다." );
  };
}

let bora = new User("이보라");

bora.sayHi(); // 내 이름은 이보라입니다.

/*
bora = {
   name: "이보라",
   sayHi: function() { ... }
}
*/
```
