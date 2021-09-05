# 자료구조와 자료형 2

# Date 객체와 날짜
- Date 내장 객체
	- 날짜를 저장할 수 있고, 날짜와 관련된 메서드도 제공해줌
	- 생성 및 수정 시간을 저장, 시간 측정, 등 다양하게 사용
## 객체 생성하기
`new Date()`를 호출하면 새로운 Date객체가 생성됨
```javascript
let now = new Date();
alert( now ); // 현재 날짜 및 시간이 출력됨
```
- timestamp : 1970의 첫날을 기준으로 흘러간 밀리초를 나타냄
- `new Date(milliseconds)`
	- UTC 기준 1970년 1월1일0시0분0초에서 밀리초 이후의 시점이 저장된 Date객체가 반환됨
- 1970년 1월 1일이전 날짜에 해당하는 타임스탬프값은 음수
- `new Date(detesting)`
	- 인수가 하나인데 문자열이라면 해당 문자열은 자동으로 구문 분석함
- `new Date(year, month, date, hours, minutes, seconds, ms)`
	- 주어진 인수를 조합해 만들 수 있는 날짜가 저장된 객체가 반환
	- 첫번째, 두번째 인수만 필수
## 날짜 구성요소 얻기
`Date` 객체의 메서드를 사용하면 연, 월, 일 등을 값을 얻을 수있음
- `getFullYear()`
- `getMonth()`
- `getDate()`
- `getHours(), getMinutes(), getSeconds(), getMilliseconds()`
- `getDay()`
- 위의 메서드는 모두 현지 시간 기준 날짜 구성요소를 반환

## 날짜 구성요소 설정하기 
*  setFullYear(year, [month], [date])
*  setMonth(month, [date])
*  setDate(date)
*  setHours(hour, [min], [sec], [ms])
*  setMinutes(min, [sec], [ms])
*  setSeconds(sec, [ms])
*  setMilliseconds(ms)
*  setTime(milliseconds)
## 자동 고침
- 자동 고침(autocorrection) : 범위를 벗어나는 값을 설정하려고 하면 잦동 고침 기능이 활성화 되어 값을 자동으로 수정
## Date 객체를 숫자로 변경해 시간차 측정하기
- date객체를 숫자형으로 변경하면 타임스탬프가 됨
```javascript
let start = new Date(); // 측정 시작

// 원하는 작업을 수행
for (let i = 0; i < 100000; i++) {
  let doSomething = i * i * i;
}

let end = new Date(); // 측정 종료

alert( `반복문을 모두 도는데 ${end - start} 밀리초가 걸렸습니다.` );
```

## Date.now()
	- Date.now()는 new Date().getTim() 과 의미론적으로 비슷하지만 객체 Date()를 만드지 않는점이 다름
	- 더 빠르고 가비지 컬렉터의 일을 덜어줌
	
## Date.parse와 문자열
-  `YYYY-MM-DDTHH:mm:ss.sssZ`
- YYYY-MM-DD : 연월일
- T  : 구분기호
- HH:mm:ss.sss : 시분초밀리초
- Z : 옵션 +-hh:mm형식의 시간을 나타냄 Z한글자는 UTF+0

# JSON과 메서드
## JSON.stringify
	- json은 값이나 객체를 나타내주는 범요 포맷
	- JSON을 데이터 교환 목적으로 사용
	- JSON.stringify - 객체를 JSON으로 바꿔줌
	- JSON.parse() JSON을 객체로 바꿔줌
```javascript

let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};

let json = JSON.stringify(student);

alert(typeof json); // 문자열이네요!

alert(json);
/* JSON으로 인코딩된 객체:
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "wife": null
}
*/
```
- JSON으로 인코딩된 객체의 특징
	- 문자열은 큰따옴표로 깜쌈
	- 객체 프로퍼티 이름은 큰 따옴표로 감쌈
- 원시값에도 적용가능
	- 객체
	- 배열
	- 원시형  : 문자형, 숫자형, 불린형값, Null
- 호출시 무시되는 프로퍼티
	- 함수플퍼티
	- 심볼형 프로퍼티 
	- 값이 undefined인 프로퍼티
```javascript
let user = {
  sayHi() { // 무시
    alert("Hello");
  },
  [Symbol("id")]: 123, // 무시
  something: undefined // 무시
};

alert( JSON.stringify(user) ); // {} (빈 객체가 출력됨)
```
## replacer로 원하는 프로퍼티만 직렬화하기
`let json = JSON.stringify(value[, replacer, space])`
- value : 인코딩하려는 값
- replacer : JSON으로 인코딩 하길 원하는 프로퍼티가 담긴 배열/함수
- space 서식 변경 목적으로 사용할 ㅤ문자수
```javascript
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: [{name: "John"}, {name: "Alice"}],
  place: room // meetup은 room을 참조합니다
};

room.occupiedBy = meetup; // room은 meetup을 참조합니다

alert( JSON.stringify(meetup, function replacer(key, value) {
  alert(`${key}: ${value}`);
  return (key == 'occupiedBy') ? undefined : value;
}));

/* replacer 함수에서 처리하는 키:값 쌍 목록
:             [object Object]
title:        Conference
participants: [object Object],[object Object]
0:            [object Object]
name:         John
1:            [object Object]
name:         Alice
place:        [object Object]
number:       23
*/
```
- replacer함수가 중첩 객체와 배열의 요소까지 포함한 모든 키-값 쌍을 처리함
## space로 가독성높이기
```javascript
let user = {
  name: "John",
  age: 25,
  roles: {
    isAdmin: false,
    isEditor: true
  }
};

alert(JSON.stringify(user, null, 2));
/* 공백 문자 두 개를 사용하여 들여쓰기함:
{
  "name": "John",
  "age": 25,
  "roles": {
    "isAdmin": false,
    "isEditor": true
  }
}
*/

/* JSON.stringify(user, null, 4)라면 아래와 같이 좀 더 들여써집니다.
{
    "name": "John",
    "age": 25,
    "roles": {
        "isAdmin": false,
        "isEditor": true
    }
}
*/
```
## 커스텀 “toJSON”
- toJSON이라는 메서드가 구현되어ㅣ 있으면 객체를 JSION으로 바꿀 수 있음
```javascript
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  date: new Date(Date.UTC(2017, 0, 1)),
  room
};

alert( JSON.stringify(meetup) );
/*
  {
    "title":"Conference",
    "date":"2017-01-01T00:00:00.000Z",  // (1)
    "room": {"number":23}             
  }
*/
```
1. date의 값이 문자열로 변환
```Javascript
let room = {
  number: 23,
  toJSON() {
    return this.number;
  }
};

let meetup = {
  title: "Conference",
  room
};

alert( JSON.stringify(room) ); // 23

alert( JSON.stringify(meetup) );
/*
  {
    "title":"Conference",
    "room": 23
  }
*/
```
## JSON.parse
- JSON으로 인코딩된 객체를 다시 객체로 디코딩 할 수 있음
- `let value = JSON.parse(str, [reviver]);`
	- str : JSON 형식의 문자열
	- reviver : (key,value)쌍을 대상으로 호출되는 함수로 값을 변경 시킬 수 있음
### 자주 저지르는 실수
```javascript
let json = `{
  name: "John",                     // 실수 1: 프로퍼티 이름을 큰따옴표로 감싸지 않았습니다.
  "surname": 'Smith',               // 실수 2: 프로퍼티 값은 큰따옴표로 감싸야 하는데, 작은따옴표로 감쌌습니다.
  'isAdmin': false                  // 실수 3: 프로퍼티 키는 큰따옴표로 감싸야 하는데, 작은따옴표로 감쌌습니다.
  "birthday": new Date(2000, 2, 3), // 실수 4: "new"를 사용할 수 없습니다. 순수한 값(bare value)만 사용할 수 있습니다.
  "friends": [0,1,2,3]              // 이 프로퍼티는 괜찮습니다.
}`;
```

## reviver 사용하기
```javascript
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str);

alert( meetup.date.getDate() ); // 에러!
```
- meetup.date의 값은 Date객체가 아니고 문자열이기때문에 에러가 발생함
```javascript
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});

alert( meetup.date.getDate() ); // 정상작동
```