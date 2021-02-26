# HTML 



### 단락 - P 

Paragraph 의 줄임말로 단락을 표현할 때 사용합니다.



```html
<html>
    <head><meta charset="utf-8"></head>
    <body>
 
<p>HyperText Markup Language, commonly referred to as HTML, is the standard markup language used to create web pages. Along with CSS, and JavaScript, HTML is a cornerstone technology, used by most websites to create visually engaging webpages, user interfaces for web applications, and user interfaces for many mobile applications.[1] Web browsers can read HTML files and render them into visible or audible web pages. HTML describes the structure of a website semantically along with cues for presentation, making it a markup language, rather than a programming language.</p>
        
    </body>
</html>
```





### 줄바꿈 - br

새로운 행에서부터 입력이 시작되도록 합니다. 

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



시각적인 줄바꿈을 표현하는 태그 일 뿐이기 때문에 단락을 나누는  p 태그의 경우 하나의 단락이라는 정보를 정확하게 나타내기 때문에 단락을 나타내려면  p 태그를 쓰는게 좋다. 



### 이미지 - img



```html
<html>
<body>
    <img src="img.jpg" height="300" alt="산 이미지" title="산 이미지">
</body>
</html>
```





### 표 - table



```html
<html>
<head><meta charset="utf-8"></head>
<body>
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
</body>
</html>
```



`<td>`  table data의 약자, 즉, 테이블의 데이터가 들어간다고 보면 된다.

`<tr>`  table  row의 약자 즉, 같은 행에 속하는 td 태그를 tr으로 묶어주면 같은 행으로 표시한다.



![image-20210226213734702](https://user-images.githubusercontent.com/42714724/109303998-ebab0c00-787e-11eb-9f71-5263f4b373f7.png)

`<thead>` table head 즉 테이블의 분류?부분 

`<tbody>` table body 

`<tfoot>` table foot 테이블에서 가장 아래쪽으로 내려감 (태그가 어느쪽에 위치하던지 상관없이!)

```html
<html>
<head><meta charset="utf-8"></head>
<body>
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
</body>
</html>
```



`<lowspan="n">` n개의 행이 병합 된다.

`<colspan="n">` n개의 컬럼이 병합 된다.



### 입력양식 - form 



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



각각의 태그에 type과 name을 부여하면, 각각의 이름값으로 서버측으로 전송 된다.



#### text box



```html
<html>
<head>
    <meta charset="utf-8">
</head>
<body>
    <form action="">
        <p>text : <input type="text" name="id" value="default value"></p>
        <p>password : <input type="password" name="pwd" value="default value"></p>
        <p>textarea :
            <textarea cols="50" rows="2">default value</textarea>
        </p>
    </form>
</body>
</html>
```

type 속성을 `text`로 주면 text값을 입력할 수 있는 박스가 생성된다.



#### option 



```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <form action="http://localhost/color.php">
            <h1>색상</h1>
            <select name="color">
                <option value="red">붉은색</option>
                <option value="black">검은색</option>
                <option value="blue">파란색</option>
            </select>
            <h1>색상2 (다중선택)</h1>
            <select name="color2" multiple> 
        선택한 value의 값이 name이라는 이름을 가지고 전송된다. multiple은 다중 선택 가능.
                <option value="red">붉은색</option>
                <option value="black">검은색</option>
                <option value="blue">파란색</option>
            </select>
            <input type="submit">
        </form>
    </body>
</html>
```

 drop down list 

제한된 공간안에서 여러개의 선택지를 선택할 수 있도록하는 기능이다.

#### 

#### radio 



```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <form action="http://localhost/order.php">
            <p>
                <h1>색상(단일선택)</h1>
                붉은색 : <input type="radio" name="color" value="red">
                검은색 : <input type="radio" name="color" value="black" checked>
                파란색 : <input type="radio" name="color" value="blue">
            </p>
        
            <p>
                <h1>사이즈(다중선택)</h1>
                95 : <input type="checkbox" name="size" value="95">
                100 : <input type="checkbox" name="size" value="100" checked>
                105 : <input type="checkbox" name="size" value="105" checked>
            </p>
            <input type="submit">
        </form>
    </body>
</html>
```



단추같은 작은 동그라미 형태의 선택 버튼 

#### button



```html
<html>
<head><meta charset="utf-8"></head>
<body>
    <form action="http://localhost/form.php">
        <input type="text">
        <input type="submit" value="전송">
        <input type="button" value="버튼" onclick="alert('hello world')">
        <input type="reset">
    </form>
</body>
</html>
```

`submit` 의 경우 페이지 이동이 있음.

`button` 의 경우 순수한 html 코드이기 때문에 다른 동작이 존재하지 않음 -> 자바스크립트와 함께 작동함.

`reset` 이 태그가 속한 form태그 안에 있는 모든 정보가 리셋된다.





#### hidden 



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



눈에 보이지 않지만 서버쪽으로 어떠한 데이터를 보낼때 사용하는 태그 

화면상에는 보이지 않지만 get방식 전송시 url로 값이 전송되기는 한다..





#### label



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



특별한 기능이 가지고 있다고 볼 수는 없지만 해당 태그를 통해 무언가의 이름표라고 알려줄 수 있다.



```html
<label for ="helloworld">hello</label>
<input id = "helloworld" type = "text" name = "hello" > 
```



#### method 



```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <form action="http://localhost/method.php" method="post">
            <input type="text" name="id">
            <input type="password" name="pwd">
            <input type="submit">
        </form>
    </body>
</html>
```



해당 form 에 있는 내용을 전송하는 방식을 나타낸다.



#### file 



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

 파일을 올리기 위한 폼태그 

전송한 파일이 서버쪽 컴퓨터에 올라간다! 

