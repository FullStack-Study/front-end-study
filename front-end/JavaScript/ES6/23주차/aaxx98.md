# 자료구조와 자료형

## 1. 원시값의 메서드

### 원시값과 객체

-   원시값

    -   원시형 값
    -   string
    -   number
    -   bigint
    -   boolean
    -   symbol
    -   null
    -   undefined

-   객체

    -   프로퍼티에 다양한 종류의 값을 저장 가능
    -   함수도 객체의 일종
    -   함수를 프로퍼티로 저장할 수 있음 (메서드)

-   객체는 내부구조를 유지하기 위해 추가 자원을 사용하기 때문에 원시값 보다 무겁다.

### 원시값을 객체처럼 사용하기

-   래퍼 객체

    -   String
    -   Number
    -   Boolean
    -   Symbol

    ```js
    let str = "Hello";

    alert(str.toUpperCase()); // HELLO
    ```

    -   메소드(함수 프로퍼티)를 실행하는 원시값 str

        -   원시값을 통해 프로퍼티에 접근하는 순간, 원시값을 알고있고 메소드를 가지고있는 래퍼 객체가 생성된다.
        -   메소드가 실행되어 결과가 반환된다.
        -   래퍼 객체는 파괴되고 원시값만 남는다.

    -   래퍼 객체의 타입은 `object`

        ```js
        alert(typeof 0); // "number"
        alert(typeof new Number(0)); // "object"!
        ```

        -   래퍼 객체를 `new` 키워드를 통해 직접 생성하면 객체가 생성됨
        -   객체는 논리평가시 true를 반환하므로 사용시 주의해야함

    -   `null`, `undefined`는 메소드가 없다.

## 2. 숫자형

### 표현법

-   10의 거듭제곱 `e`
    ```js
    1e3 = 1000
    1e-3 = 0.001
    ```
-   2진수: `0b`, 8진수: `0o`, 16진수: `0x`
    ```js
    0xff = 255
    0o377 = 255
    0b11111111 = 255
    ```

### `toString(base)`

```js
let num = 255;

alert(num.toString(16)); // ff
alert(num.toString(2)); // 11111111
```

-   `base`진법으로 `num`을 표현하고 문자형으로 변환해 반환함
    -   base는 최대 36 (숫자 0~9, 알파벳 a~z 총 36개로 표현)
-   숫자에서 직접 메소드 호출
    -   `255..toString(2)` // 점 두개
    -   `(255).toString(16)` // 괄호로 묶기

### 어림수 구하기

-   `Math.floor`: 소수점 첫째 자리에서 버림
-   `Math.ceil`: 소수점 첫째 자리에서 올림
-   `Math.round`: 소수점 첫째 자리에서 반올림
-   `Math.trunc`: 소수부 무시

-   `Number.toFixed(n))`: 숫자형 메소드, 반올림하여 소수점 n자리수까지 표현한 수를 문자열로 반환

### 부정확한 계산

-   64비트로 표현할 수 없는 너무 큰 수는 `Infinity`로 처리됨
-   소수점 정밀도 손실(이진법 소수 표현의 한계)
    ```js
    alert(0.1 + 0.2 == 0.3); // false
    alert(0.1 + 0.2); // 0.30000000000000004
    ```
-   두 종류의 0 (`0`, `-0`)
    -   대부분의 연산에서 0, -0은 동일하게 취급된다.

### isNaN과 isFinite

-   특수 숫자 값

    -   `Infinity`, `-Infinity`
        -   어떤 숫자보다 큰/작은 값
    -   `NaN`
        -   에러를 나타내는 값
    -   특수 숫자값은 숫자형에 속한다.

-   특수 숫자값을 정상적인 숫자와 구별하기 위해 메소드가 존재한다.

    -   `isNaN(value)`: 인수를 숫자로 변환하고, `NaN`인지 테스트

        ```js
        alert(isNaN(NaN)); // true
        alert(isNaN("str")); // true
        ```

        -   `NaN`은 자기자신을 포함하여 어떤 값과도 같지 않으므로 동일연산자로 판단할수 없다.

    -   `isFinite(value)`: 인수를 숫자로 변환하고, `NaN`, `Infinity`, `-Infinity`중 어느것도 아닌 일반숫자라면 true반환
        ```js
        alert(isFinite("15")); // true
        alert(isFinite("str")); // false (NaN)
        alert(isFinite(Infinity)); // false (Infinity)
        ```

### parseInt, parseFloat

-   100px, 12pt와 같이 숫자+단위로 표시된 문자열에서 숫자를 읽을 때 사용한다.
    -   `parseInt()`, `parseFloat()`은 문자열에서 불가능할 때 까지 숫자를 읽는다.
    -   숫자를 읽는 도중 오류가 발생하면 이미 수집된 숫자를 반환한다.
    -   처음부터 숫자를 읽을 수 없다면 `NaN`을 반환한다.
-   `+` 또는 `Number()`을 사용하여 숫자형으로 변형할 때, 피연산자가 숫자가 아니면 형변환에 실패한다.

## 3. 문자열

### 특수 기호

-   `\n`: 줄바꿈
-   `\r`: 캐리지 리턴
-   `\'`, `\"`, `\\` : 따옴표, 역슬래시를 출력하려면 역슬래시를 붙여야함
-   `\t` : 탭
-   `\b`,`\f`,`\v` : 백스페이스/폼피드/세로탭 (요즘 잘 사용되지 않음)
-   `\x--` : 16진수 유니코드 글자
-   `\u----`: 16진수 유니코드 기호
-   `\u{-...---}`: UTF-32 유니코드 기호

```js
alert("\u00A9"); // ©
alert("\u{20331}"); // 佫
alert("\u{1F60D}"); // 😍
```

### 문자열 길이

-   length 프로퍼티에 문자열 길이가 저장되어있다.
-   `str.length`로 접근한다.

### 특정 글자에 접근

-   n번째 글자에 접근

    -   `str[n]`
    -   `str.charAt(n)`

-   `for..of`
    -   문자열을 구성하는 글자에 순차적으로 접근
    ```js
    for (let char of "Hello") {
        alert(char); // H,e,l,l,o
    }
    ```

### 문자열의 불변성

-   문자열은 수정할 수 없다. (글자 하나만 수정 불가능)
-   수정하려면 문자열 전체를 새로 할당해야한다.

### 대/소문자 변경

-   `toLowerCase()`
    -   대문자 -> 소문자
-   `toUpperCase()`
    -   소문자 -> 대문자

### 부분 문자열

-   `~str.indexOf(substr)`: substr이 str의 부분문자열인지 확인
-   `str.includes(substr)`: substr이 str의 부분문자열인지 확인
-   `str.startsWith(sub)`: str이 sub으로 시작하는지 확인
-   `str.endsWith(sub)`: str이 sub으로 끝나는지 확인

-   `str.substring(start, end)`: start부터 end 사이의 문자열 추출
-   `str.slice(start, end)`: start부터 end 까지의 문자열 추출 (start <= end)
-   `str.substr(str, length)`: start부터 length개의 글자 추출

### 문자열 비교

-   `str.localeCompare(str2)`: 국제 표준에 따라 str과 str2 비교
    -   str < str2 : 음수 반환
    -   str = str2 : 0 반환
    -   str > str2 : 양수 반환
