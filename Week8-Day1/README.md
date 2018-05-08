# 5/8 (화)

## 1. Today I learned

### 1-1.  DOM API

#### 폼 이벤트

: form태그에는 내장기능이 있는데 이것을 활용하기도 하고 상황에 따라 없애기도 한다.

- **submit 이벤트는 폼에 전송이 일어날때 화면이 이동**하는 기본동작이 있으므로 `e.preventDefault()`가 필요하다.

```js
document.querySelector('form').addEventListener('submit', e => {
  e.preventDefault();
  alert(e.target.elements.gender.value);
  alert(e.target.elements.name.value);
})
```
- `e.target.elements` : 폼엘리먼트 객체에는 elements 라는 속성이 있다.
  - `e.target`이 폼 엘리먼트 객체를 가리키고 있다.
  - [HTMLFormElement.elements](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/elements)



- 전송버튼을 누르지 않고, **input에서 엔터키를 누르면 전송**이 된다.
  - 데이터전송뿐만 아니라 다른방법으로 활용가능하다.
  - ex. 할일 추가 목록에서 옆에 + 버튼을 누르지않아도 엔터를 치면 할일이 추가되도록 한다.



#### 마우스 이벤트

: 사용자가 사용중인 마우스의 동작으로 이벤트를 지정할 수 있다.

+ `click` / `dblclick`: 클릭 / 더블클릭
+ `mouseover` / `mouseout`: 마우스 커서가 위에 있을때 / 벗어날 때
+ `mousedown` / `mouseup`: 마우스에 있는 스위치가 내려갈때 올라갈때(클릭과 비슷)
+ `mousemove`: 마우스가 조금이라도 이동하면 동작하는 이벤트(보통 1초에 60번(**60fps**))



클릭 이벤트는 마우스 업/다운과 달리 터치에도 잘 동작한다. 그래서 보통 클릭 이벤트를 많이 사용하고 마우스 업/다운은 특별히 그 동작을 분리해야 할 때 사용한다.  
그래서 보통 마우스 업/다움은 드래그앤 드롭에 사용한다.

[devDocs - click](https://devdocs.io/dom_events/click)에서 properties를 보면 `button`,`buttons`라는 속성이 있다. 여기에 숫자로 마우스 오른쪽 스위치인지, 가운데 휠인지, 왼쪽 스위치인지 정보를 담고 있다.(이진수 버튼 연산을 공부하고 다시 보자)

이벤트에 대한 정보를 알고 싶으면 devDocs, MDN에서 문서를 찾아보자

[마우스 업/다운/무브로 만든 드래그앤 드롭 이벤트](https://codepen.io/dbeat999/pen/wjPVJv?editors=1011)
```js
const boxEl = document.querySelector('.box');

let dragging = false;
let originalOffset;
let originalMousePos;

document.addEventListener('mousemove', e => {
  if (dragging) {
    const newTop = `${originalOffset.top + (e.clientY - originalMousePos.y)}px`
    const newLeft = `${originalOffset.left + (e.clientX - originalMousePos.x)}px`
    boxEl.style.top = newTop;
    boxEl.style.left = newLeft;    
  }
  console.log(`x:${e.clientX}, y:${e.clientY}`);
});

boxEl.addEventListener('mousedown', e => {
  dragging = true;
  originalOffset = {
    top: boxEl.offsetTop,
    left: boxEl.offsetLeft
  };
  originalMousePos = {
    x: e.clientX,
    y: e.clientY
  }
})

boxEl.addEventListener('mouseup', e => {
  dragging = false;
})

```
클릭 이벤트는 마우스 업/다운과 달리 터치에도 잘 동작한다. 그래서 보통 클릭 이벤트를 많이 사용하고 마우스 업/다운은 특별히 그 동작을 분리해야 할 때 사용한다.  
그래서 보통 마우스 업/다움은 드래그앤 드롭에 사용한다.

[devDocs - click](https://devdocs.io/dom_events/click)에서 properties를 보면 `button`,`buttons`라는 속성이 있다. 여기에 숫자로 마우스 오른쪽 스위치인지, 가운데 휠인지, 왼쪽 스위치인지 정보를 담고 있다.(이진수 버튼 연산을 공부하고 다시 보자)

이벤트에 대한 정보를 알고 싶으면 devDocs, MDN에서 문서를 찾아보자

[마우스 업/다운/무브로 만든 드래그앤 드롭 이벤트](https://codepen.io/dbeat999/pen/wjPVJv?editors=1011)
```js
const boxEl = document.querySelector('.box');

let dragging = false;
let originalOffset;
let originalMousePos;

document.addEventListener('mousemove', e => {
  if (dragging) {
    const newTop = `${originalOffset.top + (e.clientY - originalMousePos.y)}px`
    const newLeft = `${originalOffset.left + (e.clientX - originalMousePos.x)}px`
    boxEl.style.top = newTop;
    boxEl.style.left = newLeft;    
  }
  console.log(`x:${e.clientX}, y:${e.clientY}`);
});

boxEl.addEventListener('mousedown', e => {
  dragging = true;
  originalOffset = {
    top: boxEl.offsetTop,
    left: boxEl.offsetLeft
  };
  originalMousePos = {
    x: e.clientX,
    y: e.clientY
  }
})

boxEl.addEventListener('mouseup', e => {
  dragging = false;
})
```
클릭 이벤트는 마우스 업/다운과 달리 터치에도 잘 동작한다. 그래서 보통 클릭 이벤트를 많이 사용하고 마우스 업/다운은 특별히 그 동작을 분리해야 할 때 사용한다.  
그래서 보통 마우스 업/다움은 드래그앤 드롭에 사용한다.

[devDocs - click](https://devdocs.io/dom_events/click)에서 properties를 보면 `button`,`buttons`라는 속성이 있다. 여기에 숫자로 마우스 오른쪽 스위치인지, 가운데 휠인지, 왼쪽 스위치인지 정보를 담고 있다.(이진수 버튼 연산을 공부하고 다시 보자)

이벤트에 대한 정보를 알고 싶으면 devDocs, MDN에서 문서를 찾아보자

[마우스 업/다운/무브로 만든 드래그앤 드롭 이벤트](https://codepen.io/dbeat999/pen/wjPVJv?editors=1011)
```js
const boxEl = document.querySelector('.box');

let dragging = false;
let originalOffset;
let originalMousePos;

document.addEventListener('mousemove', e => {
  if (dragging) {
    const newTop = `${originalOffset.top + (e.clientY - originalMousePos.y)}px`
    const newLeft = `${originalOffset.left + (e.clientX - originalMousePos.x)}px`
    boxEl.style.top = newTop;
    boxEl.style.left = newLeft;    
  }
  console.log(`x:${e.clientX}, y:${e.clientY}`);
});

boxEl.addEventListener('mousedown', e => {
  dragging = true;
  originalOffset = {
    top: boxEl.offsetTop,
    left: boxEl.offsetLeft
  };
  originalMousePos = {
    x: e.clientX,
    y: e.clientY
  }
})

boxEl.addEventListener('mouseup', e => {
  dragging = false;
})
```



#### 키보드 이벤트

: 사용자가 입력한 키보드의 동작 상태나 특정 키를 눌렀을때의 브라우저 이벤트를 지정할 수 있다. 

- `keydown` / `keyup`  : 키가 눌렸을 때, 키가 떼어졌을때
  - keydown 에서 e.key 를 통해서 어떤 키가 눌렸는지 알 수 있다. 
  - [mdn - key value](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values)

**html**

```html
<input type="text" value="">
```

**js**

```js
inputEl = document.querySelector('input[type=text]');

inputEl.addEventListener('keydown', e => {
  console.log('keydown : ' + e.key);
  if (e.key === 'ArrowUp' ){
      console.log('위쪽 화살표')  
    }else if (e.key === 'ArrowLeft' ){
      console.log('왼쪽 화살표')  
    }
});

inputEl.addEventListener('keyup', e => {
  console.log('keyup');
});

// document.addEventListener('keyup', e => {
//  console.log('keyup : '+ e.key );
// });

// 키보드 이벤트는 document에도 사용가능하다.
```



 

#### 스크롤 이벤트

: 브라우저내에서 스크롤이 발생했을 경우 스크롤을 움직일때마다 이벤트가 발생한다.

- `scroll`

```js
// 스크롤을 움직일 때마다 이벤트가 발생함.

document.addEventListener('scroll', e => {
  console.log('scroll' + window.scrollY);
});
```



---



### 1-2.  BEM(Block Element Modifier)

+ [BEM Quick start](https://en.bem.info/methodology/quick-start/)
+ [css방법론(1) - BEM](https://medium.com/witinweb/css-%EB%B0%A9%EB%B2%95%EB%A1%A0-1-bem-block-element-modifier-1c03034e65a1)



####  클래스 이름 짓는 방법  

 자바스크립트에서 확신을 가지게 해주는 요소가 있으면 프로그래밍하기 좋다.  
확신을 가지게 하는 요소: 스코프  
(함수의 매개변수는 코드 밖에서 쓸 수 없다. 함수 안에서만 유효하다. -> 다른 함수의 영역을 침범하지 않는다.  
매개변수가 전역변수처럼 사용된다면, 어디서 어떻게 변할지 확신할 수 없는 상황이 된다. 구조적으로 분리해서 생각할 수 있게 해준다.)

CSS는 스코프라는 개념이 없다. CSS에서 선언하는 클래스명은 모두 전역 변수처럼 사용된다.  
클래스 이름을 일반명사(예: `.form`, `.section`)로 쓰지 않아야한다. 좀 더 구체적으로, 명시적으로 만들어줘야 한다.

프로그래밍 언어처럼 사람이 직접 스코프 같은 처리를 해줘야한다.  
이러한 처리를 위한 방법론(단, 기계가 직접 처리해주는 방법도 있다.)



#### 작명규칙(Naming Convertion)

- css선택자 이름을 가능한 명확하게 하는것이 목표
- 소문자, 숫자만을 사용한다.
- 여러단어 조합은 하이픈(-)으로 연결한다.



##### 블록(Block)

- 재사용 할 수 있는 기능적으로 독립적인 페이지 구성요소
- 형태가 아닌 목적에 맞게 결정해야 함
- 블록은 환경에 영향을 받지 않아야 함. (여백이나 위치를 설정하면 안됨)
- 태그, id 선택자를 사용하면 안됨
- 블록은 서로 중첩해서 작성 가능



##### 요소(Element)

- 블록안에서 특정 기능을 담당함
- bolck__element 형태로 사용 (더블 언더바)
- 형태가 아닌 목적에 맞게 결정해야함
- 요소는 중첩해서 작성 가능
- 요소는 블록의 부분으로만 사용할 수 있음
- 모든 블록에서 요소는 필수가 아닌 선택적으로 사용 (ex) menu__item, header__title...



##### 수식어(Modifier)

- 블록이나 요소의 모양, 상태를 정의함
- block__element--modifier, block--modifier 형태로 사용(더블 하이픈)
- 수식어의 블리언 타입과 키-벨류 타입이 있음
- 블리언 타입 : 수식어가 있으면 값이 true라고 가정함 (form__button--disabled)
- 키-벨류 타입 : 키, 벨류를 하이픈으로 연결하여 표시함 (color-red, theme-oceam)
- 수식어는 단독으로 사용할 수 없음. 즉 기본 블록과 요소에 추가하여 사용해야 함 (class="block__element block__element--modifier")



##### 혼합사용 (Mix)

- block1, block2__element 형태로 사용가능
- block2__element 에 여백이나 위치를 지정하고 block1은 독립적으로 유지가능




```html
<form action="" class="login-form">
  아이디<input type="text" class="login-form__id-input">
  암호<input type="text" class="login-form__password-input">
</form>


<form action="" class="login-form login-form--vip">
  아이디<input type="text" class="login-form__id-input">
  암호<input type="text" class="login-form__password-input">
</form>
```



- BEM은 클래스명이 길게 이어지다보니 바로 css로 작성하는것 보다 sass나 less를 이용하는것이 효율적이다.

- BEM은 엄청 많은 내용(파일 구조까지도...)을 담고 있는 방법론이다.  
  이를 다 지키긴 어렵고 적절히 다른 방법론과 섞어 사용하는 경우도 있고, 클래스 명을 짓는 경우에만 적용하는 경우도 있다.

  

---



### 1-3. Sass

Sass는 CSS pre-processor로 css의 복잡한 작업을 쉽게 할 수 있게 해주고, 코드의 재활용성을 높여주며, 코드의 가독성을 높여주어 유지보수를 쉽게 해준다. Sass는 SASS 문법과 SCSS문법이 있는데 현업에서 가독성이 더 좋은 SCSS문법을 더 많이 쓴다.

vscode의 **Live Sass Compiler**라는 확장 프로그램을 설치하면 Sass/SCSS파일을 바로 CSS로 컴파일해준다. 



#### 변수(Variables)

컬러나 폰트 스택같이 재사용할 값들을 변수에 저장해 사용할 수 있다.

##### SCSS

```scss
// 아래의 예제는 모두 SCSS이다. 
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```
##### 컴파일된 css

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```



#### 중첩(Nesting)

Sass 에서는 부모요소의 자식요소를 스타일링 할 때 부모 스코프 내에 종속이 가능하여 코드량을 줄일 수 있다.

##### SCSS

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```
##### 컴파일된 css
```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```



#### 부모 참조 선택자(`&`)

& 는 내가 방금 썼던 선택자를 나타낸다. 반복되는 글자를 계속 써야하는 번거로움을 없애준다. 

##### SCSS

```scss
.home-anchor {
  color: green;
  // 부모 참조 선택자
  &:hover {
    color: red;
  }
  &:visited {
    color: purple;
  }
}
```
##### 컴파일된 css
```css
.home-anchor {
  color: green;
}

.home-anchor:hover {
  color: red;
}

.home-anchor:visited {
  color: purple;
}
```



부모 참조 선택자를 사용하면 BEM을 다음과 같이 사용할 수 있다.

##### SCSS
```scss
.login-form {
  &__id-input {
    caret-color: red;
  }
  &__password-input {
    caret-color: blue;
  }
  &--vip &__id-input{
    background-color: gold;
  }
```
##### 컴파일된 css
```css
.login-form__id-input {
  caret-color: red;
}

.login-form__password-input {
  caret-color: blue;
}

.login-form--vip .login-form__id-input {
  background-color: gold;
}
```



---



## 2. Today I found out

드래그 앤 드롭 구현하는 예제에서 쉬는시간에 어떻게 구현해야 moveup이 되었을 때 mousemove의 동작을 해제 시킬 수 있을까 remmoveEventListenr를 써볼 수는 없을까 고민했는데 결국 생각하지 못했다. 그 다음 시간에 dragging이라는 변수 하나를 추가해 if문에 dragging의 값으로 조건을 걸어 dragging의 상태는 mousemove이벤트 밖의 moveup, mousedown에서 처리하는 것을 보고 이렇게 생각하는 방법도 있다는 걸 깨달았다.  
Sass 처음 배울 때 Sass 컴파일 하려고 루비도 깔고, 나중에는 Node Sass 나왔대서 Node.js 깔고 gulp 쓰면 다른 처리도 자동화 해준대서 gulp도 깔았는데, visual studio code에는 이 Sass의 컴파일을 해주는 확장 프로그램이 있다는 것을 처음 알았다.  
현업에서야 gulp나 webpack같은 자동화 도구나 빌드 툴을 사용하겠지만, 확장 프로그램만으로 컴파일이 간단해져 쉽게 Sass를 복습해볼 수 있게 되었다.

