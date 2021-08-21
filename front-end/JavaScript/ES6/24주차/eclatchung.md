# 210820

생성일: 2021년 8월 20일 오후 8:01

## 배열

### 배열의 내부 동작 원리

배열은 특별한 종류의 객체입니다. 다만, 키가 숫자라는 점만 다름

### 성능

- `pop` 과 `push` 는 빠르지만, `shift` 와 `unshift` 는 느림
- shift연산 과정
	1. 인덱스가 0인 요소를 제거
	2. 모든 요소를 왼쪽으로 이동
	3. length 프로퍼티 값을 갱신
	4. 배열에 요소가 많으면 요소가 이동하는데 걸리는 시간이 길고 메모리 관련 연산도 많아짐

### length

- 배열에 무언가 조작을 가하면 자동으로 length 프로퍼티가 자동으로 갱신
- length를 쓰기가 가능함
	- 증가 시키면 아무런 일이 생기지 않음
	- 감소 시키면 배열이 짤림

### toString

- 배열엔 toString 메서드가 구현되어 있음.
- 쉼표로 구분된 문자열이 반환
- `Symbol.toPrimitive` / `valueOf` 메서드는 없음

## 배열과 메서드

### 요소 추가 / 제거 메서드

- `arr.push()` : 맨 끝에 요소 추가
- `arr.pop()` : 맨 끝 요소 제거
- `arr.shift()` : 맨 앞 요소 제거
- `arr.unshift()` : 맨 앞 요소 추가

### splice

- 배열에서 요소를 하나 지우고 싶을 때 사용
- delete를 배열에 사용하면 삭제는되지만, length는 그대로가 됨.
	- delete는 key를 이용해 해당 키에 상응하는 값을 지움

arr.splice(index[, deleteCount, elem1, .., elemN])

- index
- deleteCount : 제거하고자 하는 요소의 개수
- elem1 ..elemN : 배열에 추가할 요소

let arr = ["I", "study", "JavaScript", "right", "now"];

// 처음(0) 세 개(3)의 요소를 지우고, 이 자리를 다른 요소로 대체합니다.
arr.splice(0, 3, "Let's", "dance");

alert( arr ) // now ["Let's", "dance", "right", "now"]

- splice는 삭제된 요소로 구성된 배열을 반환

### slice

arr.slice([start],[end])

- start 인덱스 부터 (end인덱스를 제외한) end 인덱스까지의 요소를 복사한 새로운 배열을 반환
- start, end 둘다 음수일 때 배열 끝에서부터의 요소의 갯수를 의미

### concat

arr.concat(arg1, arg2...)

- arr에 속한 모든 요소와 arg1, arg2등에 속한 모든 요소를 한데 모은 새로운 배열이 반환
- 인수 argN가 배열일 경우 배열의 모든 요소가 복사.

let arr = ["I", "study", "JavaScript", "right", "now"];

// 처음(0) 세 개(3)의 요소를 지우고, 이 자리를 다른 요소로 대체합니다.
arr.splice(0, 3, "Let's", "dance");

alert( arr ) // now ["Let's", "dance", "right", "now"]

- concat 메서드는 제공받은 배열의 요소를 복사해 활용
	- 객체가 인자로 넘어오면 객체는 분해되지 않고 통으로 복사되어 더해짐
	- Symbol.isConcatSpreadable이 있으면 concat은 객체를 배열처럼 취급

### forEach로 반복 작업

arr.forEach(function(item, index, array) {
  // 요소에 무언가를 할 수 있습니다.
});

### 배열 탐색하기

- indexOf, lastIndexOf, includes
	- arr.indexOf(item, from)는 인덱스 from , item을 찾음 → 요소를 발견하면 해당 요소의 인덱스를 반환하고 발견하지 못했으면 -1을 반환함
	- arr.lastIndexOf(item, from)는 위 메서드와 동일한기능을 하는데, 검색을 끝에서부터 시작한다는 점만 다름
	- arr.includes(item, from)는 인덱스 from부터 시작해 item이 있는지 검색하고, 해당하는 요소를 발견하면 true 반환
- find / findIndex

let result = arr.find(function(item, index, array) {
  // true가 반환되면 반복이 멈추고 해당 요소를 반환합니다.
  // 조건에 해당하는 요소가 없으면 undefined를 반환합니다.
});

- find
	- item : 함수를 호출할 요소
	- index : 요소의 인덱스
	- array : 배열 자기 자신
	- 함수가 참을 반환하면 탐색은 중단되고 요소가 반환.
	- 요소를 찾지 못하면 undefined가 반환

### filter

- find 메서드는 함수의 반환값을 true로 만드는 단 하나의 요소를 찾음
- 조건을 충족하는 요소가 여러 개라면 arr.filter(fn)를 사용
- 조건에 맞는 요소 전체를 담은 배열을 반환

### 배열을 변형하는 메서드

- map
	- 배열 요소 전체를 대상으로 함수를 호출하고 함수 호출 결과를 배열로 반환
- sort(fn)
	- 배열의 요소를 정렬
	- 배열 자체가 변경
	- 메서드 호출하면 재정렬된 배열이 반환이되는데, arr 자체가 수정되어서 반환값은잘 사용하지 않음
- reverse
	- arr의 요소를 역순으로 정렬시켜주는 메서드
- split / join
	- split은 긴 문자열의 형태의 수신자 리스트를 배열 형태로 전환하여 처리시 사용
	- split의 두 번째 인수로 숫자를 받을 수 있음 → 배열의 길이를 제한해줌
- reduce / reduceRight
	- 배열을 기반으로 값 하나를 도출할 때 사용
	- accumulator : 이전 함수 호출의 결과 initial은 함수 최초 호출시 사용되는 초깃값을 나타냄
	- item : 현재 배열 요소
	- index : 요소의 위치
	- array : 배열

let value = arr.reduce(function(accumulator, item, index, array) {
  // ...
}, [initial]);

let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current, 0);

alert(result); // 15

### Array.isArray 로 배열 여부 알아내기

- 배열은 js에서 객체로 구분되어 typeof으로는 배열 여부를 알아 낼 수 없음
- Array.isArray 로 배열을 구분할 수 있음

### 배열 메서드와 'thisArg'

- sort제외 대부분의 배열 메서드는 thisArg라는 매개변수를 옵션으로 받을 수 있음
- thisArg는 func의 this가 됨

let army = {
  minAge: 18,
  maxAge: 27,
  canJoin(user) {
    return user.age >= this.minAge && user.age < this.maxAge;
  }
};

let users = [
  {age: 16},
  {age: 20},
  {age: 23},
  {age: 30}
];

// army.canJoin 호출 시 참을 반환해주는 user를 찾음
let soldiers = users.filter(army.canJoin, army);

alert(soldiers.length); // 2
alert(soldiers[0].age); // 20
alert(soldiers[1].age); // 23

- thisArgs에 army를 지정하지 않고 단순히 `user.filter(army.canJoin)` 을 사용했다면 army.canJoin은 단독 함수처럼 취급되고 함수 본문내의 this는 undefined되어 에러 발생

## iterable 객체

- 반복 가능한 객체는 배열을 일반화한 객체
	- 이터럴블(반복가능한)이라는 개념을 사용하면 어떤 객체에든 `for...of` 반복문을 적용할 수 있음
	- 배열은 다표적인 이터러블, 문자열도 이터러블의 예
	- 배열이 아닌 객체가 있는데 이 객체가 어떤것들의 컬렉션(목록, 집합 등)을 나타내고 있는 경우 `for ..of` 을 사용하면 컬렉션 순회하는데 유용

### Symbol.iterator

let range = {
  from: 1,
  to: 5
};

range를 이터러블로 만들면 객체에 `Symbol.iterator` 라는 메서드를 추가해 아래와 같은 이벤트가 발생하게 해야함

1. for.. of가 시작되자 마자  for.. of는 `Symbol.iterator` 를 호출. `Symbol.iterator` 는 반드시 이터레이터를 반환해야함
2. 이후 for ..of는 반환된 객체(이터레이터)만을 대상으로 동작
3. for..of에 다음 값이 필요하면 for .. of는 이터레이터의 next() 메서드 호출
4. next()의 반환값은 {done:Boolean, value :any}와 같은 형태여야함. done=true는 반복이 종료되었음을 의미. done=false일 때 value에 다음 값이 저장.

let range = {
  from: 1,
  to: 5
};

// 1. for..of 최초 호출 시, Symbol.iterator가 호출됩니다.
range[Symbol.iterator] = function() {

  // Symbol.iterator는 이터레이터 객체를 반환합니다.
  // 2. 이후 for..of는 반환된 이터레이터 객체만을 대상으로 동작하는데, 이때 다음 값도 정해집니다.
  return {
    current: this.from,
    last: this.to,

    // 3. for..of 반복문에 의해 반복마다 next()가 호출됩니다.
    next() {
      // 4. next()는 값을 객체 {done:.., value :...}형태로 반환해야 합니다.
      if (this.current <= this.last) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
};

// 이제 의도한 대로 동작합니다!
for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}

- range에는 메서드 next()가 없음
- range[Symbol.iterator]를 호출해서 만든 이터레이터 객체와 이 객체의 메서드 next()에서 반복에 사용될 값을 만듬
- 이터러블 객체의 핵심 ⇒ `관심사의 분리`

let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  alert(num); //1, then 2,3,4,5
}

- this.current에 반복이 얼마나 진행되었는지 나타내는 값이 저장됨
- 코드 짧아짐
- 단점 : 하나의 객체에 동시에 for ..of 반복문을 사용할 수가 없음

### 이터레이터를 명시적으로 호출하기

let str = "Hello";

// for..of를 사용한 것과 동일한 작업을 합니다.
// for (let char of str) alert(char);

let iterator = str[Symbol.iterator]();

while (true) {
  let result = iterator.next();
  if (result.done) break;
  alert(result.value); // 글자가 하나씩 출력됩니다.
}

이터레이터를 명시적으로 호출하는 경우는 없는데, 이방법을 사용시에 반복과정을 잘 통제할 수있다는 장점이 있음

### 이터러블과 유사 배열

- 이터러블 : 메서드 Symbol.iterator가 구현된 객체
- 유사 배열(arrya-like) : 인덱스와 length프로퍼티가 있어서 배열 처럼 보이는 객체

let arrayLike = { // 인덱스와 length프로퍼티가 있음 => 유사 배열
  0: "Hello",
  1: "World",
  length: 2
};

// Symbol.iterator가 없으므로 에러 발생
for (let item of arrayLike) {}

### Array.from

- 이터러블이나 유사 배열을 받아 진짜 `Array` 로 만들어줌
- 객체를 받아 이터러블이나 유사 배열인지를 조사하여 넘겨받은 인수가 이터러블이나 유사배열인 경우 새로운 배열을 만들고 객체의 모든 요소를 새롭게 만든 배열로 복사.

## 맵과 셋

### 맵

- 맵은 키가 있는 데이터를 저장한다는 점에서 객체와 유사
- 다양한 자료형을 허용한다는 점에서 차이
- `new Map()`
- `map.set(key, value)` - key를 이용하여 value 저장
- `map.get(key)` - key에 해당하는 값을 반환 key 존재 하지 않으면 undefined 반환
- `map.has(key)` - 키가 존재하면 true, 존재하지 않으면 false를 반환
- `map.delete(key)` - key에 해당하는 값을 삭제
- `map.clear()` - 맵 안의 모든 요소 제거
- `map.size` - 요소의 개수를 반환

let map = new Map();

map.set('1', 'str1');   // 문자형 키
map.set(1, 'num1');     // 숫자형 키
map.set(true, 'bool1'); // 불린형 키

// 객체는 키를 문자형으로 변환한다는 걸 기억하고 계신가요?
// 맵은 키의 타입을 변환시키지 않고 그대로 유지합니다. 따라서 아래의 코드는 출력되는 값이 다릅니다.
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3

### 맵의 요소에 반복 작업하기

- `map.keys()` – 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환
- `map.values()` – 각 요소의 값을 모은 이터러블 객체를 반환
- `map.entries()` – 요소의 `[키, 값]`을 한 쌍으로 하는 이터러블 객체를 반환합니다. 이 이터러블 객체는 `for..of`반복문의 기초로 쓰입니다.

### Object.entries : 객체를 맵으로 바꾸기

- 각 요소가 키-값쌍인 배열이나 이터러블 객체를 초기화 용도로 맵에 전달해 새로운 맵을 만들 수 있음

let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));

alert( map.get('name') ); // John

### Object.fromEntries : 맵을 객체로 바꾸기

let prices = Object.fromEntries([
  ['banana', 1],
  ['orange', 2],
  ['meat', 4]
]);

// now prices = { banana: 1, orange: 2, meat: 4 }

alert(prices.orange); // 2

### 셋(set)

- 중복을 허용하지 않는 값을 모아놓은 특별한 컬렉션
- `new Set(iterable)` - 대게 배열을 전달받음
- `set.add(value)` – 값을 추가하고 셋 자신을 반환
- `set.delete(value)` – 값을 제거, 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 `true`, 아니면 `false`를 반환
- `set.has(value)` – 셋 내에 값이 존재하면 `true`, 아니면 `false`를 반환
- `set.clear()` – 셋을 비움
- `set.size` – 셋에 몇 개의 값이 있는지 카운트함

### 셋의 값에 반복작업하기

let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// forEach를 사용해도 동일하게 동작합니다.
set.forEach((value, valueAgain, set) => {
  alert(value);
});