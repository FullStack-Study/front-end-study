# 자료구조와 자료형

## 워크맵과 위크셋

- 자바스크립트는 도달 가능한 값을 메모리에 유지
- `맵`에서 객체를 키로 사용한 경우, `맵`이 메모리에 있는 한 객체는 메모리에 남음
	- 가비지 컬렉터의 대상이 되지 않음
``` javascript
let john = { name: "John" };

let map = new Map();
map.set(john, "...");

john = null; // 참조를 null로 덮어씀

// john을 나타내는 객체는 맵 안에 저장되어있습니다.
// map.keys()를 이용하면 해당 객체를 얻는 것도 가능합니다.
for(let obj of map.keys()){
  alert(JSON.stringify(obj));
}

alert(map.size);
```

### 위크맵
- 위크맵을 사용시 키로 쓰인 객체가 가비지 컬렉션의 대상
- 위크맵의 키가 반드시 객체여야함
```javascript
let weakMap = new WeakMap();

let obj = {};

weakMap.set(obj, "ok"); //정상적으로 동작합니다(객체 키).

// 문자열("test")은 키로 사용할 수 없습니다.
weakMap.set("test", "Whoops"); // Error: Invalid value used as weak map key
```

- 맵과 위크맵의 차이
	- 키가 반드시 객체여야함
	- 반복작업 지원안함
	- 아래의 메서드 지원안함 
		- keys()
		- values()
		- entries()
- 위크맵 지원 메서드
	- weakMap.get(key)
	* weakMap.set(key, value)
	* weakMap.delete(key)
	* weakMap.has(key)
#### 유스 케이스 : 추가 데이터
- 부차적인 데이터를 저장할 곳이 필요할 때 사용
### 유스 캐이스 : 캐싱
- 캐싱이 필요할 때 유용
- 캐싱은 시간이 오래 걸리는 작업의 결과를 저장하여 연산 시간과 비용을 절약해주는 기법
### 위크셋
- 위크셋과 셋은 유사하지만, 객체만 저장 할 수 있다는 점이 다름
- 셋 안의 객체는 도달 가능할때만 메모리 유지
- add, has, delete, size, keys()나 반복작업 관련 메서드는 사용할 수 없음


## Object.keys, values, entries
- `keys()`, `values()`, `entries()` 
	- `Map`
	- `Set`
	- `Array`
- 일반객체의 메서드
	-  Object.keys(obj)  – 객체의 키만 담은 배열을 반환함
	*  Object.values(obj)– 객체의 값만 담은 배열을 반환함
	*  Object.entries(obj) – [키, 값] 쌍을 담은 배열을 반환함

- 맵
	- 호출 문법 
		- map.keys)
	- 반환값
		- iterable 객체
- 객체
	- 호출문법
		- Object.keys(obj)
	- 반환값
		- ‘진짜’ 배열

1. `obj.keys()`가 아닌 `Object.keys(obj)`를 호출
	- 어떠한 객체에 구체적으로 객체이름.values()라는 메서드를 구현할 수 도 있음
2. 메서드 Object.*를 호출하면 iterable객체가 아닌 객체의 한 종류인 배열을 반환한다는 점

### 객체 변환하기
- 객체엔 map, filter같은 배열전용메서드를 사용할 수 없음
- `Object.entries`, `Object.fromEntries`를 순차적으로 적용하면 객체에도 배열 전용 메서드를 사용할 수 있음.
```javascript
let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

let doublePrices = Object.fromEntries(
  // 객체를 배열로 변환해서 배열 전용 메서드인 map을 적용하고 fromEntries를 사용해 배열을 다시 객체로 되돌립니다.
  Object.entries(prices).map(([key, value]) => [key, value * 2])
);

alert(doublePrices.meat); 
```

## 구조분해할당 
- 키를 가진 데이터 여러 개를 하나의 엔티티에 저장할 땐 객체를 사용
- 컬렉션에 데이터를 순서대로 저장할 땐 배열을 사용
- 구조 분해 할당 (destructuring assignment)는 객체나 배열을 변수로 분해해주는 특별한 문법 구조

### 배열 분해하기
```javascript
// 이름과 성을 요소로 가진 배열
let arr = ["Bora", "Lee"]

// 구조 분해 할당을 이용해
// firstName엔 arr[0]을
// surname엔 arr[1]을 할당하였습니다.
let [firstName, surname] = arr;

alert(firstName); // Bora
alert(surname);  // Lee
```

#### ‘…’로 나머지 요소 가져오기
배열 앞쪽에 위치한 값 몇개만 필요하고 그 이후 이어지는 나머지 값을 한데 모아서 저장시 사용
```javascript
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert(name1); // Julius
alert(name2); // Caesar

// `rest`는 배열입니다.
alert(rest[0]); // Consul
alert(rest[1]); // of the Roman Republic
alert(rest.length); // 2
```
- 할당할 값이 없으면 undefined로 취급함

### 객체 분해하기
```javascript
let {var1, var2} = {var1:…, var2:…}
```

### 중첩 구조 분해
- 객체나 배열이 다른 객체나 배열을 포함 시 더 복잡한 패턴을 사용하면 중첩 배열이나 객체의 정보를 추출하는 문법
```javascript
let options = {
  title: "My menu",
  items: ["Item1", "Item2"]
};

function showMenu({
  title = "Untitled",
  width: w = 100,  // width는 w에,
  height: h = 200, // height는 h에,
  items: [item1, item2] // items의 첫 번째 요소는 item1에, 두 번째 요소는 item2에 할당함
}) {
  alert( `${title} ${w} ${h}` ); // My Menu 100 200
  alert( item1 ); // Item1
  alert( item2 ); // Item2
}

showMenu(options);
```