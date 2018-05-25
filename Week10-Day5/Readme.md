# 5/25 (금)

## 1. Today I learend

---

## 1. [DocumentFragment](https://developer.mozilla.org/ko/docs/Web/API/DocumentFragment)

> DocumentFragment는 일반적으로 DOM 서브트리를 조립해서 DOM에 삽입하기 위한 용도로 사용되고, 이 때 `appendChild()`나 `insertBefore()` 같은 Node 인터페이스의 메소드가 사용됩니다.  
이 작업은 **fragment의 노드들을 DOM으로 이동시키고, DocumentFragment를 비웁니다** `appendChild()` Fragment 자체가 인수로 들어가는 게 아니라 그 안에 객체만 받아오고 한번 쓰면 비워지기 때문에, 계속 쓰려면 변수에 담아서 써야한다.
## 2. for문과 분해대입

### 2.1. forEach

```js
res.data.forEach(async ({id, body, complete}) => {
  console.log(id)
  console.log(body)
  console.log(complete)
})

// forEach를 쓴다면 forEach 인자 역시 함수이므로 `await`를 쓰려면 `async`를 붙여줘야한다.
```

### 2.2. for ... of
- `forEach` `for of`를 쓸 때, 분해대입으로 객체 안에 있는 속성별로 가져와서 쓸 수 있다. `forEach`는 함수 이기 때문에 async를 붙여서 써야하는 반면 `for of`루프는 비동기 함수를 자연스럽게 섞어 쓸 수 있다.

```js
for(const {id, body, complete} of res.data) {
  console.log(id)
  console.log(body)
  console.log(complete)
}
```

## 3. loading 인디케이터, Promise

Promise 객체를 인수로 받는 로딩 인티케이터 표시 함수  
**비동기 함수는 Promise 객체를 반환한다.**
```js
async function withLoading(promise) {
  rootEl.classList.add('root--loading');
  const value = await promise;
  rootEl.classList.remove('root--loading');
  return value;
}
```

## 4. Boolean 어트리뷰트 

```js
checkboxEl.setAttribute('checked', '')
```

```html
<input type="checkbox" checked>
```

## 5. 디버깅

개발자 도구나 vs code에서 가능하다.

+ [debugger](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/debugger)

코드내 중단점에 `debugger`를 추가하여 개발자 도구에서 디버깅 할 수 있다.  
(개발자 도구 내에서도 중단점을 지정할 수 있다.)  

`Debugger`처럼 Source탭에서 해당 라인을 선택해서 새로고침하면 똑같이 동작. VScode에서 디버거for크롬 확장 설치해서 사용 가능.
```js
function render(fragment) {
  rootEl.textContent = '';
  debugger;
  rootEl.appendChild(fragment);
}
```

+ vs code에 [Debbugger for Chrome](https://github.com/Microsoft/vscode-chrome-debug) 확장프로그램을 설치하여 사용할 수 있다.
```json
{
  // IntelliSense를 사용하여 가능한 특성에 대해 알아보세요.
  // 기존 특성에 대한 설명을 보려면 가리킵니다.
  // 자세한 내용을 보려면 https://go.microsoft.com/fwlink/?linkid=830387을(를) 방문하세요.
  "version": "0.2.0",
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "Launch Chrome",
      "url": "http://localhost:1234",
      "webRoot": "${workspaceFolder}/src"
    }
  ]
}
```

## 6. [BLUAMA](https://bulma.io/)

부트스트랩이나 meterial design component같은 프레임워크는 CSS와 JavaScript 둘다 포함되어 있지만 **BLUMA**는 CSS만 제공한다.

cdnjs에서 min.css 맨 윗줄 링크에 적용

아이콘 제공 방식(제작 난이도) png sprite < svg sprite < icon font
