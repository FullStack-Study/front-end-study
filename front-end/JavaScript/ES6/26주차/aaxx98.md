# Date 객체와 날짜

## 내장객체 Date

-   날짜를 저장할 수 있고, 날짜와 관련된 메서드를 제공함
-   사용 예시
    -   생성/수정 시간 저장
    -   시간 측정
    -   현재 날짜 출력

### 객체 생성

-   `new Date()`
    -   인수 없이 호출시, 현재 날짜와 시간이 저장된 Date객체가 반환됨
-   `new Date(ms)`
    -   UTC 기준 1970/1/1에서 `ms`밀리 초 후의 시점이 저장된 Date 객체가 반환됨
    -   1970/1/1 이전 시간은 음수값을 넣어 사용한다.
-   `new Date(string)`
    -   `new Date("2017-01-26");`
    -   문자열이 자동 구문분석 된다.
-   `new Date(year, month, date, hours, minutes, seconds, ms)`
    -   `year`: 네자리 숫자
    -   `month`: 0(1월)~11(12월) 사이의 숫자
    -   `date`: 기본값 1
    -   그외: 기본값 0

### 날짜 구성요소 얻기

-   현지 시간 기준 날짜 구성 요소를 반환하는 메서드
    -   `getFullYear()`
        -   네자릿수 연도 반환
        -   `getYear()`은 deprecated인 비표준 메서드이므로 사용하지 않는 것이 좋다.
    -   `getMonth()`
        -   월 반환 (0~11)
    -   `getDate()`
        -   일 반환
    -   `getHours()`, `getMinutes()`, `getSeconds()`, `getMilliseconds()`
        -   시, 분, 초, 밀리초 반환
    -   `getDay()`
        -   요일 반환
-   표준시(UTC+0) 기준 날짜 구성 요소를 반환하는 메서드
    -   위 메서드 이름에 `getUTCDay()`와 같이 UTF를 붙여 사용한다.
    -   `getTime()`
        -   메서드를 호출한 Date 객체와 1970/1/1 0시 0분 0초 사이의 밀리초 간격(타임스탬프) 반환
    -   Date 객체를 숫자형으로 형변환하면 타임스탬프가 반환된다.
    -   `getTimezoneOffset()`
        -   현지시간과 표준시간의 차이(분) 반환

### 날짜 구성요소 설정

-   setFullYear(year, [month], [date])
-   setMonth(month, [date])
-   setDate(date)
-   setHours(hour, [min], [sec], [ms])
-   setMinutes(min, [sec], [ms])
-   setSeconds(sec, [ms])
-   setMilliseconds(ms)
-   setTime(milliseconds)

### 자동 고침

```js
let date = new Date(2013, 0, 32);
alert(date); // Fri Feb 01 2013 00:00:00 GMT+0900 (한국 표준시)
```

-   n일 후, n초 전/후의 Date을 얻을 수 있다.

    ```js
    let date = new Date(2016, 1, 28);
    date.setDate(date.getDate() + 2);

    alert(date); // Tue Mar 01 2016 00:00:00 GMT+0900 (한국 표준시)
    ```

### `Date.now()`

-   Date 객체를 생성하지 않고 현재 타임스탬프를 반환
    -   `new Date().getTime()`과 반환 결과가 같다.
    -   객체를 만들지 않기 때문에 가비지 컬렉터의 일을 덜어준다.

### `Date.parse(str)`

-   문자열 형식 `YYYY-MM-DDTHH:mm:ss.sss[옵션]`
    -   `YYYY-MM-DD` : 날짜 연-월-일
    -   `T`: 구분자
    -   `HH:mm:ss.sss` : 시간 시:분:초.밀리초
    -   `[옵션]`: `+-hh:mm` 형식 시간대를 나타내는 옵션 (기본값 UTC+0)

# JSON과 메서드

-   `JSON.stringify`: 객체를 JSON으로 변환

    -   객체 뿐만 아니라 원시값에도 적용 가능하다.
    -   객체는 문자열로 변환 된 후에 네트워크를 통해 전송하거나, 저장될 수 있다.
        -   JSON으로 인코딩된 / 직렬화 처리된 / 문자열로 변환된 / 결집된 객체
    -   무시되는 객체 내 프로퍼티
        -   함수 프로퍼티 (메서드)
        -   심볼형 프로퍼티 (key가 심볼)
        -   값이 undefinded인 프로퍼티
    -   중첩 객체도 문자열로 변환된다.

        -   순환 참조가 있으면 변환 불가능하다.

            ```js
            let room = {
                number: 23,
            };

            let meetup = {
                title: "Conference",
                participants: ["john", "ann"],
            };

            meetup.place = room; // meetup -> room
            room.occupiedBy = meetup; // room -> meetup

            JSON.stringify(meetup); // Error: Converting circular structure to JSON
            ```

    -   `let json = JSON.stringify(value[, replacer, space])`

        -   `value`: 인코딩 하려는 객체
        -   `replacer`: JSON으로 인코딩하기 원하는 프로퍼티가 담긴 배열 또는 매핑 함수 `function(key, value)`

            -   매핑 함수

                ```js
                let room = {
                    number: 23,
                };

                let meetup = {
                    title: "Conference",
                    participants: [{ name: "John" }, { name: "Alice" }],
                    place: room,
                };

                room.occupiedBy = meetup; // stringify에서 무시되는 프로퍼티

                alert(
                    JSON.stringify(meetup, function replacer(key, value) {
                        alert(`${key}: ${value}`);
                        return key == "occupiedBy" ? undefined : value; // undefined를 반환하면 직렬화에 포함시키지 않는다.
                    })
                );
                ```

        -   `space`: 서식 변경 목적으로 사용할 공백 문자 수
            -   가독성을 위해 들여쓰기 공백 개수를 지정한다.

    -   `toJSON()`

        -   객체 내부에 `toJSON` 메서드가 구현되어 있으면 `JSON.stringify`를 호출했을 때 `toJSON`이 실행된다.

            ```js
            let room = {
                number: 23,
                toJSON() {
                    return this.number;
                },
            };

            let meetup = {
                title: "Conference",
                room,
            };

            alert(JSON.stringify(room)); // 23

            alert(JSON.stringify(meetup));
            /*
            {
                "title":"Conference",
                "room": 23
            }
            */
            ```

-   `JSON.parse`: JSON을 객체로 변환

    -   `let value = JSON.parse(str, [reviver]);`

        -   `str`: JSON 형식 문자열

            -   JSON 형식은 문자열로 표현된다.

                -   프로퍼티는 큰 따옴표로 감싼다.
                -   문자열 값은 큰 따옴표로 감싼다.
                -   순수값만으로 표현한다.

        -   `reviver`: 모든 key-value 쌍에 대해 호출되는 `function(key, value)` 함수

            ```js
            let str =
                '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

            let meetup = JSON.parse(str, function (key, value) {
                if (key == "date") return new Date(value); // key가 date이면 Date 객체 반환
                return value;
            });

            alert(meetup.date.getDate());
            ```
