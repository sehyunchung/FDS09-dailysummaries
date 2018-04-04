### 오늘의 퀴즈
1) carousel a.k.a slide image js 없이 작동x   
3) `<track>`    
label 속성으로 텍스트에 사용될 색상을 정할 수 있다.   
Label > in information   
5) `grid-area`   
grid-row-start -> grid-column-start -> grid-row-end -> grid-column-end 순서  

 

6) 텍스트와 배경의 명도 대비는 4.5 대 1 ~~이어야 한다~~ **이상**이어야 한다.   
---
## JS 간단 개념 
```
>Library: 자주 쓰는 기능을 모아놓은 곳 ex) Jquery(vs Native 방식: 일일이 구현)
>
>DOM: API의 일종으로 화면의 요소요소를 객체화하여 접근할 수 있게 함
>
>(window.)document.getElementByTag 나 querySelector 등을 이용하여 해당 객체의 값을 가지고 오거나 접근!
```
## defer
```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Web Cafe</title>
  <link rel="stylesheet" href="css/style.css">
  <script src="js/jquery.min.js"></script>
  <script src="js/webcafe.js"></script>
</head>
```
 브라우저가 html을 파싱하여  DOM구조를 만들기 전에 스크립트가 먼저 실행되었으므로, 위 코드로는  js가 브라우저에서 실행되지 않는다.    
그래서 일반적으로 `</body>` 태그 뒤에 `<script>` 태그로 js파일을 삽입하여, 문서의 파싱 작업을 완료한 후 스크립트 파일을 실행하도록 하는 것이다.  <br>
```Html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Web Cafe</title>
  <link rel="stylesheet" href="css/style.css">
  <script defer src="js/jquery.min.js"></script>
  <script defer src="js/webcafe.js"></script>
</head>
```
위의 코드와 같이 HTML5 와 ES6에서는 script 태그에 `defer` 속성을 삽입하여 `<body>` 태그 전에 스트립트를 선언하면 브라우저에서 `</body>` 태그 뒤에 `<script>` 태그로 js파일을 삽입하는 것과 동일하게 작동한다.   <br>
[브라우저의 파싱 및 DOM에 대한 보충설명 참조]<br>[http://poiemaweb.com/js-dom#3-dom-query--traversing-%EC%9A%94%EC%86%8C%EC%97%90%EC%9D%98-%EC%A0%91%EA%B7%BC]
---



### In Form.html

```html
<input type="radio" name="mailing" value="no" id="mailing-no" title="메일링 리스트에 가입여부">
```

name - 서버에서 데이터를 handling하기 위한 속성

title - 대체 텍스트를 위한 속성

#seulbi.github.io - day8<br>

- `Clear fix `<br>
    - float한 요소의 **부모**에 준다.
      -float(혹은 block)을 쓸 시, 영향 받은 요소가 block형태로 변하여 width값 변경 가능
- figure 속 img삽입시 효과 구분하여주기!
  <br>
### calc( )  
> calc() 는 값을 계산해주는 표현식이다. 
>
> 두개의 요소를 화면에 배치할때 한 요소의 크기를 자동으로 계산하여 나머지크기를 화면에 배치할 때 쓰는 함수!
>
> `+` `-` `*` `/` 연산자를 조합하여 구성한다.   
```Css
/* 속성: calc(표현식) */
width: calc(100% - 80px);
/* 연산자 앞/뒤 반드시 **공백**을 포함하여야 한다. */
```

### white-space   
> 어떤 요소(element; 부모요소) 안의 공백(whitespace)이 어떻게 처리될지를 나타내는데 사용된다.   
>
> 이 속성의 기본값은 `normal`이고 모든 요소에 적용된다.   <br>
```css
/* white-space 속성 값들 */
white-space: normal;   
/* 연속된 공백이 하나로 병합, 소스 안의 줄바꿈 문자는 다른 공백 문자와 같이 취급. 텍스트 줄바꿈 o */   
white-space: nowrap;  
/* normal 과 같이 공백 문자를 병합하지만, 텍스트 줄바꿈(text wrapping)을 하지 않음.*/
white-space: pre;   
/* 연속된 공백이 보존됨. 줄은 오로지 소스의 줄바꿈 문자나 <br> 요소에서만 끊어짐.*/   
white-space: pre-wrap;   
/* 연속된 공백이 보존. 줄은 줄바꿈 문자, <br>, 그리고 줄 박스를 채우기 위해 필요에 따라 끊어짐.*/   
white-space: pre-line;   
/* 연속된 공백이 병합 */
```
[white-space 의 특징을 한눈에 알아보자!]<br>[https://mdn.mozillademos.org/ko/docs/Web/CSS/white-space$samples/See_in_action?revision=1219723]
<br>
### Text-overflow
> 박스안의 내용이 넘칭 때 텍스트를 어떻게 처리할 것인지 지정하는 속성.  
> `text-overflow` 속성은 다음 2가지 조건일 경우에만 적용된다    
> - overflow 속성값이 hidden, scroll, auto 일 때(visible 제외)   
> - White-space: nowrap 일 경우, 또는 텍스트가 다음 줄로 이동하지 않는 비슷한 경우    
```Css
/* text-overflow의 속성값 */
text-overflow: clip;
/* 텍스트를 잘라냄 */
text-overflow: ellipsis;
/* 오늘 배운 '...': 문장이 길때 뒤의 중간을 생략하고 ...을 넣어줄 수 있음 */
text-overflow: "…";
/* "" 안에 지정한 문자열을 표시한다. */
```

### article vs section ###
```html
>Article: 그 자체가 독립적 의미 가짐. RSS 피드로 보낼 가치가 있는 경우 사용한다.
>
>Section: 어떤 영역의 하위 의미를 전달하는 부분
[<article> <section> 의 차이][http://aboooks.tistory.com/346]
<br>
```
Float issue 해결 4가지
1. `clear fix` 해당 부모요소고려하여 주기!
2. 부모요소도 같이 float주기
3. `overflow: hidden/ scroll`
4. `clear:both;` 값을 float영향을 안받고 싶은 요소에다 주기!