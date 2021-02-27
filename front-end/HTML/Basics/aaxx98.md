# HTML
Hyper Text Markup Language
웹 문서를 만들기 위해 사용하는 기본적인 웹 언어의 한 종류
태그를 이용하여 데이터의 속성을 정의하고, 태그를 중첩하여 페이지를 작성할 수 있다.

## 1. 문서의 구조
`head`와 `body`
- `head`: 본문이 아닌 내용 (title, meta 태그 등)
- `body`: 본문에 해당되는 내용
-  `head`와 `body`는 `html` 태그로 감싼다.
```html
<html>
<head>
  <title>HTML - 수업소개</title>
  <meta charset="utf-8">
</head>
<body>
<h1>HTML</h1>
<ol>
  <li>기술소개</li>
  <li>기본문법</li>
  <li>하이퍼텍스트와 속성</li>
  <li>리스트와 태그의 중첩</li>
</ol>
 
<h2>선행학습</h2>
 
본 수업을 효과적으로 수행하기 위해서는 웹애플리케이션에 대한 전반적인 이해가 필요합니다. 이를 위해서 준비된 수업은 아래 링크를 통해서 접근하실 수 있습니다. 
</body>
</html>
```

## 2. DOCTYPE
Document type declaration

어떤 방식의 html 언어로 작성한 파일인지 선언해야한다.

가장 최근의 html 버전인 HTML5를 이용해 작성했다면 `<!DOCTYPE html>`을 선언하면 된다.

## 3. 주요 태그
- `<p>` : 단락(peragraph)을 표현할 때 사용한다.
    ```html
    <html>
    <head><meta charset="utf-8"></head>
    <body>
 
    <p>단락1</p>
    <p>단락2</p>

    </body>
    </html>
    ```
- `<br>` : 강제 줄바꿈(a forced line-break)을 할 때 사용한다. 새로운 행에서 내용이 시작되도록 한다.

*p 태그 내에서의 단락을 나눌 때는 br 태그를 쓰는것 보다 새로운 p 태그로 단락을 시작하는 것이 적절하다.*

    ```html
    <html>
    <head><meta charset="utf-8"></head>
    <body>
    HyperText Markup Language, commonly referred to as HTML, is the standard markup language used to create web pages. Along with CSS, and JavaScript, HTML is a cornerstone technology, used by most websites to create visually engaging webpages, user interfaces for web applications, and user interfaces for many mobile applications.[1] Web browsers can read HTML files and render them into visible or audible web pages. HTML describes the structure of a website semantically along with cues for presentation, making it a markup language, rather than a programming language.<br><br><br>
    
    HTML elements form the building blocks of all websites. HTML allows images and objects to be embedded and can be used to create interactive forms. It provides a means to create structured documents by denoting structural semantics for text such as headings, paragraphs, lists, links, quotes and other items.<br><br><br>
    
    The language is written in the form of HTML elements consisting of tags enclosed in angle brackets. Browsers do not display the HTML tags and scripts, but use them to interpret the content of the page<br><br><br>

    </body>
    </html>
    ```

- `<img>` : 이미지 태그

    이미지를 나타내는 태그, 속성은 다음과 같다.
    - src: 이미지의 위치
    - height: 세로(px)
    - width: 가로(px)
    - alt: 이미지를 대체하는 정보 텍스트
    - title: 이미지 도움말

    ```html
    <img src="img.jpg" height="300" alt="산 이미지" title="산 이미지">
    ```
- `<table>` : 표
    - `<td>` : table data
    - `<tr>` : table row
    <table border="2">
    <tr>
        <td>이름</td>     <td>성별</td>   <td>주소</td>
    </tr>
    <tr>
        <td>최진혁</td>  <td>남</td>      <td >청주</td>
    </tr>
    <tr>
        <td>최유빈</td>  <td>여</td>      <td>청주</td>
    </tr>
    </table>

    ```html
    <table border="2">
        <tr>
            <td>이름</td>     <td>성별</td>   <td>주소</td>
        </tr>
        <tr>
            <td>최진혁</td>  <td>남</td>      <td >청주</td>
        </tr>
        <tr>
            <td>최유빈</td>  <td>여</td>      <td>청주</td>
        </tr>
    </table>
    ```

    *(border는 테이블 테두리 속성)*
    다음과 같이 표를 작성할 수 있다. 




    - `<thead>` : table head (분류), 분류는 `<th>`로 표시한다.
    - `<tbody>` : table body (테이블 가운데에 위치)
    - `<tfoot>` : table foot (테이블 가장 아래 위치)

    <table border="2">
    <thead>
        <tr>
            <th>이름</th>     <th>성별</th>   <th>주소</th> <th>회비</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>최진혁</td>  <td>남</td>      <td >청주</td> <td>1000</td>
        </tr>
        <tr>
            <td>최유빈</td>  <td>여</td>      <td>청주</td> <td>500</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>합계</td>  <td></td>      <td></td> <td>1500</td>
        </tr>
    </tfoot>
    </table>


    ```html
    <table border="2">
        <thead>
        <tr>
            <th>이름</th>     <th>성별</th>   <th>주소</th> <th>회비</th>
        </tr>
        </thead>
        <tbody>
            <tr>
                <td>최진혁</td>  <td>남</td>      <td >청주</td> <td>1000</td>
            </tr>
            <tr>
                <td>최유빈</td>  <td>여</td>      <td>청주</td> <td>500</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>합계</td>  <td></td>      <td></td> <td>1500</td>
            </tr>
        </tfoot>
    </table>
    ```
    
     - 테이블 셀 병합: `<td>`에 속성을 작성한다.
        - rowspan: 위아래로 합칠 셀 갯수
        - colspan: 좌우로 합칠 셀 갯수

        <table border="2">
            <thead>
                <tr>
                    <th>이름</th>     <th>성별</th>   <th>주소</th> <th>회비</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>최진혁</td>  <td>남</td>      <td rowspan="2">청주</td> <td>1000</td>
                </tr>
                <tr>
                    <td>최유빈</td>  <td>여</td>      <td>500</td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td colspan="3">합계</td>      <td>1500</td>
                </tr>
            </tfoot>
        
        </table>

        ```html
        <table border="2">
            <thead>
                <tr>
                <th>이름</th>     <th>성별</th>   <th>주소</th> <th>회비</th>
            </tr>
            </thead>
            <tbody>
                <tr>
                    <td>최진혁</td>  <td>남</td>      <td rowspan="2">청주</td> <td>1000</td>
                </tr>
                <tr>
                    <td>최유빈</td>  <td>여</td>      <td>500</td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td colspan="3">합계</td>      <td>1500</td>
                </tr>
            </tfoot>
        </table>
        ```

    ## 4. 정보 입력
    ### form
    정보를 입력하고, 전송할 수 있는 단위
    - `action` 속성: form의 내용을 보내고자 하는 주소
    - `<input>`: `type` 속성에 따라 데이터를 입력 가능한 형태로 나타난다.
        - `name` 속성: form 내에 포함된 각각의 control(입력창)을 식별하기 위한 이름

        ```html
        <html>
        <head>
            <meta charset="utf-8">
        </head>
        <body>
        <form action="http://localhost/login.php">
            <p>아이디 : <input type="text" name="id"></p>
            <p>비밀번호 : <input type="password" name="pwd"></p>
            <p>주소 : <input type="text" name="address"></p>
            <input type="submit">
        </form>
        </body>
        </html>
        ```
        - `type` 속성: 입력 양식을 정의한다.
            - `type = "text"` : 텍스트 입력
            - `type = "password"` : 비밀번호 입력
            - `type = "radio"` : 라디오 버튼 (단일 선택)
            - `type = "checkbox"` : 체크 박스 (복수 선택)
    
    
    - `<text area>`: 텍스트를 입력할 수 있는 넓은 입력창이 생성된다.
        - cols, rows 속성을 지정하면 크기를 설정할 수 있다.
        ```html
        <p>textarea :
            <textarea cols="50" rows="2">default value</textarea>
        </p>
        ```

    - `<select>` : drop down 선택창이 생성된다.
        - `<option>`: drop down 항목들을 작성한다.
        ```html
        <select name="color">
            <option value="red">붉은색</option>
            <option value="black">검은색</option>
            <option value="blue">파란색</option>
        </select>
       ``` 
        - `multiple` 속성을 추가하면 다중 선택이 가능한 창이 생성된다.
        ```html
         <select name="color">
            <option value="red">붉은색</option>
            <option value="black">검은색</option>
            <option value="blue">파란색</option>
        </select>
        ```
    
    - radio 버튼: name이 같은 radio 타입 input들 중에서 하나만 선택 될 수 있다. checked는 기본 선택이 되도록하는 속성이다. 선택된 input의 value가 전달된다.

        붉은색 : <input type="radio" name="color" value="red">
        검은색 : <input type="radio" name="color" value="black" checked>
        파란색 : <input type="radio" name="color" value="blue">

        ```html
        붉은색 : <input type="radio" name="color" value="red">
        검은색 : <input type="radio" name="color" value="black" checked>
        파란색 : <input type="radio" name="color" value="blue">
        ```
    - check box: name이 같은 checkbox 타입 input이 여러개 선택 될 수 있다.  checked는 기본 선택이 되도록하는 속성이다. 선택된 input의 value가 전달된다.

        95 : <input type="checkbox" name="size" value="95">
        100 : <input type="checkbox" name="size" value="100" checked>
        105 : <input type="checkbox" name="size" value="105" checked>

        ```html
        95 : <input type="checkbox" name="size" value="95">
        100 : <input type="checkbox" name="size" value="100" checked>
        105 : <input type="checkbox" name="size" value="105" checked>
        ```

    - 버튼: `onclick` 속성에 기능을 추가할 수 있다. 버튼을 클릭하면 onclick에 할당된 내용이 실행됨

     <input type="button" value="버튼" onclick="alert('hello world')">

     ```html
     <input type="button" value="버튼" onclick="alert('hello world')">
     ```
     
     - `<label>`: control의 제목을 설정할 때 사용한다.
        - input에 id값을 정해주고, label의 for 속성에 id를 할당하면 label의 텍스트가 input에 포함된다.
     ```html
    <form action="http://localhost/hidden.php">
        <label for="id_txt">text</label>
        <input id="id_txt" type="text" name="id">
        <label for="pw_txt">password</label>
        <input id="pw_txt" type="hidden" name="hide" value="egoing">
        <input type="submit">
    </form>
     ```
        label 안에 텍스트와 input을 포함하는 방식도 가능하다.
     ```html
    <form action="http://localhost/hidden.php">
        <label>text
        <input id="id_txt" type="text" name="id">
        </label>
        <label>password
        <input id="pw_txt" type="hidden" name="hide" value="egoing">
        </label>
        <input type="submit">
    </form>
     ```


### hidden, 안보이는 데이터 전송
input 태그의 type이 hidden인 경우
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <form action="http://localhost/hidden.php">
            <input type="text" name="id">
            <input type="hidden" name="hide" value="egoing">
            <input type="submit">
        </form>
    </body>
</html>
```

`<input type="hidden" name="hide" value="egoing">` input은 화면에 드러나지 않지만 서버로는 hide=egoing이라는 데이터가 전송된다.

### method
- get 방식: 서버쪽으로 데이터를 전송할 때 url에 data가 표시된다.
- post 방식: 서버쪽으로 데이터를 전송할 때 url에 data가 표시되지 않는다.
method는 form의 속성으로 지정해 줄 수 있다. 지정하지 않으면 get 방식으로 지정됨

```html
<form action="http://localhost/method.php" method="post">
    <input type="text" name="id">
    <input type="password" name="pwd">
    <input type="submit">
</form>
```

### 파일 업로드
input type을 file로 지정하면 파일을 선택할 수 있다.
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <form action="http://localhost/upload.php" method="post" enctype="multipart/form-data">
            <input type="file" name="profile">
            <input type="submit">
        </form>
    </body>
</html>
```