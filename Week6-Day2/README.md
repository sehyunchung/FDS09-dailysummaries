- - - 
<!-- **********************날짜************************** -->
# 042418   


# <strong> 1. References / Summary </strong>
___


- Date 를 이용한 시간 간격 측정하기 
  ```
  const start = new Date(); // 또는 Date.now(), getTime()
  const end = new Date();
  end - start;              // 3420 mili-sec 단위로 출력
  ```
  
<br />  
- moment.js 라이브러리를 이용한 시계시간 표기

> https://momentjs.com/

<br />
- Generator 함수를 활용한 라이브러리 

> https://github.com/redux-saga/redux-saga

<br />
- redux saga

> [redux-saga](https://github.com/redux-saga/redux-saga).
> [what is redux](https://voidsatisfaction.github.io/2017/02/24/what-is-redux/)




<br /><br />
# <strong> 2. Today I learned </strong>
____

<!-- *********************첫번째 제목********************** -->
## <span style="color:#595EFF"> [JS] 1-1. JSON 이해 </span>  
### Serialization 직렬화 Deserialization 역직렬화 ###

> 데이터 전송을 위한 저장/전송 가능한 형태로 바뀌주는 절차

JSON : 최근 가장 많이 사용되는 형식. 이름에서부터 JS에 의한 JS를 위한..


```
// JSON.stringify 직렬화 -> 'undefined' 속성 무시
JSON.stringify({
  key: 'value',
  arr: [1, 2, 3],
  nullProp: null
}); 

// JSON.parse 역직렬화
JSON.parse('{"key":"value","arr":[1,2,3],"nullProp":null}');
```

> 직렬화를 하고 나면 더 이상 `객체`가 아니라 `텍스트` 로 변환됨.

JSON의 속성이름을 쓸 때는 항상 `""` 큰 따옴표 사용.

<br />
#### 개념 정리 ####
___
#### 직렬화 

객체를 직렬화하여 전송 가능한 형태로 만들어 주는 것을 말하며,<br/>
객체들의 데이터를 연속적인 데이터로 변형하여 Stream 을 통해 데이터를 읽도록 해줍니다.<br/>
주로 객체들을 통채로 파일로 저장하거나 전송하고 싶을 때 주로 사용됩니다.<br/>
<br/>

#### 역직렬화 
직렬화된 파일 등을 역으로 직렬화하여 다시 객체의 형태로 만드는 것을 의미합니다.<br/>
저장된 파일을 읽거나 전송된 스트림 데이터를 읽어 원래 객체의 형태로 복원합니다.<br/>





<br /><br />
###  JSON DATE 객체 다루기  ###
___

```
const today = new Date() // data 매소드 쓴 시간이 today 에 fixed
today.getTime() // unixTime 기준으로 저장. 22332200300
const unixTime = today.getTime()
new Date(unixTime) // 2018-04-23T15:00:00.000Z
```

> 데이트 객체는 문자열이 아니다.

이를 문자열로 바꾸기 위해서는 `obj.toUTCString()`

```
const now = new Date();
console.log(now.toUTCString()); // Sun, 10 Dec 2017 03:49:31 GMT
```

<br />
moment.js 활용 예제

```
const moment = require("moment")
moment.locale('ko');

const now = moment();
console.log(now.format("dddd, MMMM Do YYYY, h:mm:ss a")); // 일요일, 12월 10일 2017, 1:02:42 오후
console.log(now.subtract(7, 'days').calendar()); // 2017.12.03
console.log(moment("20120101", "YYYYMMDD").fromNow()); // 6년 전
```





<br /><br />
### Symbol 이해 : 객체 속성이름 호출 구문 구조 ###
___


symbol 은 `배열과 똑같이 동작하는 객체를 만들 때 활용될 수 있다` <br> 
[] instanceof obj // true 로 만들 수 있다. 


- ES2015에서 도입된 새로운 원시 타입
- `Symbol` 내장 함수를 통해 새 심볼을 생성할 수 있음
- 새로 생성된 심볼은 다른 모든 심볼과 다른 것으로 취급된다.
- 객체의 속성 이름으로 사용되려고 만들어짐
- 마개조를 할 때 쓰임


> 현재 단계에서는 심볼에 대해 자세하게는 몰라도 아래 코드활용은 반드시 익힐 것.

```
const propName = 'age'
obj = {
  [propName]: 10;
}

obj // {age:10}
obj.propName // undefined
obj[propName] // 10
obj['age'] // 10
obj.age // 10
```

#### symbol 속성 알아보기 

* `Symbol.hasInstance` - 객체가 instanceof 연산자의 피연산자로 왔을 때의 동작을 바꿉니다.<br/>
* `Symbol.isConcatSpreadable` - 객체가 Array.prototype.concat 메소드의 인수로 넘겨질 때의 동작을 바꿉니다.<br/>
* `Symbol.iterator` - 객체가 for...of 구문을 통해 사용될 때의 동작 방식을 바꿉니다.<br/>
* `Symbol.match` - 객체가 String.prototype.match 메소드의 인수로 넘겨질 때의 동작을 바꿉니다.<br/>
* `Symbol.replace` - 객체가 String.prototype.replace 메소드의 인수로 넘겨질 때의 동작을 바꿉니다.<br/>
* `Symbol.search` - 객체가 String.prototype.search 메소드의 인수로 넘겨질 때의 동작을 바꿉니다.<br/>
* `Symbol.species` - Array.prototype 을 상속받은 객체에 대해 Array.prototype.map 등의 메소드를 호출할 때, 반환되는 객체의 생성자를 지정합니다.<br/>
* `Symbol.split` - 객체가 String.prototype.split 메소드의 인수로 넘겨질 때의 동작을 바꿉니다.<br/>
* `Symbol.toPrimitive` - 객체가 원시 타입의 값으로 변환되어야 할 때, 정확이 어떤 값으로 변환되어야 하는 지를 지정합니다.<br/>
* `Symbol.toStringTag` - Object.prototype.toString() 메소드를 객체에 대해 직접 호출할 때의 동작을 바꿉니다.<br/>
* `Symbol.unscopable` - with 블록 안에서 어떤 속성을 참조할 수 있는 지를 지정합니다.<br/>





<br /><br />
### Map : 처리 속도가 느린 내장 객체를 대신하여 나온 방안 ###
___

> Front-end 에서는 사용할 일이 적음. 수정이 빈번, 처리 속도가 빨라야하는 경우에 사용됨.

```
const m = new Map();

m.set('hello', 'world');
console.log(m.get('hello')); // 'world'
console.log(m.has('hello')); // true

m.delete('hello');
```


객체와 Map 객체의 차이점

- 객체는 `속성 접근자` ex. obj.name 로 컨트롤.
- Map 은 `메소드` ex. Map.set() 를 통해 컨트롤.

Map의 장점

- Map 객체의 데이트가 추가/삭제가 빈번하게 일어날 경우 훨씬 좋음
- 어떤 값이든 ex. num type 도 `속성 키` 가 될 수 있음. (속성 이름)
- Map 객체 안에 들어있는 데이터는 `프로토타입`의 영향을 받지 않음

- [fake-array](https://repl.it/@seungha/fake-array)






<br /><br />
### Set : 집합 형태의 배열 중복 허용 불가 ###
___

> Front-end 에서는 사용할 일이 적음. JSON 에서 변환이 잘 안 됨.

Set 정리

- 중복 허용 안 함
- 순서 중요하지 않음
- 값만 존재

<br />
Set을 활용한 배열안 중복제거 후, 새 배열 만들기

```
const s = new Set([1,2,3,1,2,3,4]);
const newStr = Array.from(s)    // [1,2,3,4]
```




<br /><br />
### Iterable : 반복 가능한 객체 ###
___

Generator 함수를 이용하여 커스터마이즈된 `이터러블` 함수를 만들어 호출할 수 있다. 

```
function* numberGen() {
  yield 1;
  yield 2;
  yield 3;
}

// 1, 2, 3이 순서대로 출력됩니다.
for (let n of numberGen()) {
  console.log(n);
}
```

> generator 함수에서 yield 속성은 일반 함수의 return 과 같은 역할을 한다.

<br />
- **generator로 만들어진 iterable은 오직 한번만 사용가능**
- [redux-saga](https://github.com/redux-saga/redux-saga). data communicate library.
- [what is redux](https://voidsatisfaction.github.io/2017/02/24/what-is-redux/)


어떤 객체가 Iterable 이라면, 그 객체에 대해서 아래의 기능을 사용 가능

* for...of 루프
* spread 연산자 (...)
* 분해대입(destructuring assignment)
* 기타 iterable 을 인수로 받는 함수

즉, 문자열에 대해서도 위 기능들을 사용할 수 있습니다.<br/>

```js
// `for...of`
for (let c of "hello") {
  console.log(c);
}

// spread 연산자
const characters = [..."hello"];

// 분해대입
const [c1, c2] = "hello";

// `Array.from`은 iterable 혹은 array-like 객체를 인수로 받습니다.
Array.from("hello");
```



<br /><br />
### Class : 프로토타입 벗어나기 ###
___

class 를 사용하면 prototype 에 대한 완벽한 이해가 없어도 99% 비슷하게 사용할 수 있다. 

기존에 `프로토타입`을 활용한 생성자 함수 

```js
function Person({name, age}) {
  this.name = name;
  this.age = age;
}
```

위와 동일한 `클래스`를 이용한 함수

```js
class Person {
   // 이전에서 사용하던 생성자 함수는 클래스 안에 `constructor`라는 이름으로 정의한다.
  constructor({name, age}) {
    this.name = name;
    this.age = age;
  }
```

> 객체에서 메소드를 정의할 때 사용하던 문법을 그대로 사용하면, 메소드가 자동으로 `Person.prototype`에 저장된다

<br />
class 블록에서는 JavaScript 의 다른 곳에서는 사용되지 않는 별도의 문법으로 코드를 작성해야 한다

#### 함수 혹은 객체의 내부에서 사용하는 문법과 혼동하지 않도록 주의!!

클래스는 함수가 아닙니다!

```js
class Person {
  console.log('hello');
}
// 에러: Unexpected token
```

클래스는 객체가 아닙니다!

```js
class Person {
  prop1: 1,
  prop2: 2
}
// 에러: Unexpected token
```


생성자 와 클래스의 동작 방식 차이점 :

- 클래스는 함수로 호출될 수 없음
- 클래스 선언은 let 과 const 처럼 블록 스코프에 선언되며, 호이스팅(hoisting) 발생 안 됨.
- 클래스의 메소드 안에서 super 키워드를 사용 가능
  - super : 상속시 객체의 부모가 가지고 있는 함수를 호출할 수 있게 도와주는 키워드
  
  
  

<br />
- 클래스는 `super` 메소드를 사용 가능

- **[What’s the Difference Between Class & Prototypal Inheritance?](https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9)**

- **[[Javascript ] 프로토타입 이해하기](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67)**






<br></br>
<!-- ***********************두번째 제목******************** -->
## <span style="color:#595EFF"> [JS] 2-1. Code  </span>

<br /><br />
### Generator & yield 함수 활용 예제 ###
___


#### 제너레이트 함수를 사용하게 된 가장 메인 목적은 `반복` 그리고 `for .. of` 루프를 사용하기 위해서 ####

```
// Generator 함수를 이용한 등차수열 생성하기
function* range(start = 0, end = Infinity, step = 1) {
  for (let i = start; i < end; i += step) {
    yield i;
  }
}

for(let i of range(0,10)){
  console.log(i)
}
```
> 0, 1, 2, 3, ... 8, 9

```
// 피보나치 수열 생성하기
function* fibonacci(count = Infinity) {
  let x = 1;
  let y = 1;
  for (let i = 0; i < count; i++) {
    yield x;
    [x, y] = [y, x + y];
  }
}
```

```
// 하나의 항목을 계속 넘겨주기
function* repeat(item, count = Infinity) {
  for (let i = 0; i < count; i++) {
    yield item;
  }
}
```

```
// 여러 요소를 반복해서 넘겨주기
function* repeatMany(array) {
  while (true) {
    for (let item of array) {
      yield item;
    }
  }
}
```




<br /><br />
### 직렬화 그리고 역직렬화 코드 예제 ###
___

stringify의 몇가지 옵션

```js
// 1. 콜백함수로 컨트롤
let jsonText = JSON.stringify(book, function(key, value) {
  switch (key) {
    case "authors":
      return value.json(",");
    case "year":
      return 2000;
    default:
      return value;
  }
});

// 2. 문자열 들여쓰기, 들여쓰기가 지정되어 저장됨 자동으로 줄바꿈
let jsonText = JSON.stringify(book, null, 4);
// 3. toJSON() 메서드사용
let book = {
  title: "bookname",
  authors: ["Kendrick"],
  edition: 3,
  year: 2011,
  toJSON: function() {
    return this.title;
  }
};

// stringify()시 순서는 아래와 같다
// 1. toJSON()값이 있으면 호출하여 사용
// 2. 두번째 매개변수 있다면 필터 적용
// 3. 새번째 매개변수가 있다면 그에 따라 형식 조절
```
<br />
parse의 옵션

```js
let book = {
  title: "bookname",
  authors: ["Kendrick"],
  edition: 3,
  year: 2011,
  releaseDate: new Date(2011, 11, 1)
};
let jsonText = JSON.stringify(book);
// JSON.parse()시 알아서 json스트링이 객체로 파싱
let bookCopy = JSON.parse(jsonText, function(key, value) {
  if (key == "releaseDate") {
    return new Date(value);
  } else {
    return value;
  }
});
```




<br /><br />
### Date 객체를 이용하여 알림 간단히 구현하기 ###

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <style>
        h3 {color : pink;
            border : pink solid 2px;
            width : 285px;}
    </style>
    <title>알람 어플리케이션</title>
  </head>
  <body onload = "CurrentTime()">
    현재 시간 : <input type="text", id="curTime" /><br /><br />
    알람 시간 : <input type="text", id="alhour" style="width:40px;" /> 시
              <input type="text", id="almin"  style="width:40px;" /> 분
    <h3>시간을 입력해 주세요 (예 : 14시 20분)</h3>
  </body>  
</html>
```

```js
function CurrentTime() {
  let time = new Date();
  cHour = time.getHours();
  cMin = time.getMinutes();
  cSec = time.getSeconds();
  document.querySelector("#curTime").value = cHour + ":" + cMin + ":" + cSec;
  let nalhour = Number(document.querySelector("#alhour").value);
  let nalmin = Number(document.querySelector("#almin").value);
  if (cHour == nalhour && cMin == nalmin) alert("이제 시간 됬어요!!");
  else setTimeout("CurrentTime()", 1000);
}
console.log(new Date());
console.log(setTimeout("CurrentTime()", 1000));
```





<br></br>
# <strong> 3. Today I found out </strong>
___

- 어떤 웹 앱이든 반드시 필요한 date 함수에 대해 알 수 있어서 좋았고, 수업 때 알려주신 moment.js 라이브러리에 대해 공부해보고, 차후에 포토폴리오에 반영해보면 좋을 것 같다. 

- react 를 위해 generator 함수에 대한 이해가 요구된다고 하니, 이 부분에 대해서도 관련 ref 를 찾아보면 좋을 것 같다.

- es2015에 도입된 새로운기능들이 정말 많다고 다시한번 느끼게 되는 오늘 수업이었고 실무에서는 새로도입되는 기술들이 바로바로 적용되지는 않을것 같지만,쉴틈없이 변화하는 프론트엔드의 새로운 기술들은 항상 관심있게 볼 필요가 많은 것 같다.

- es2015와 es5는 완전 다른 언어 같다. 열심히 공부해야겠다. 개발자는 스스로 고통 받는 존재라고 하던데 꽤나 잘 표현한게 아닐까. 

- 프론트엔드는 쉽지 않은 것 같다. 물론 모두 어렵겠지만 넓은 것에 대한 이해는 고집보다도 열정으로 하는 것이 아닐까. 

- 빠르고 작은 존재가 크고 무거운 존재를 이기는 것은 오직 프론트엔드가 아닐까 한다.

- 불과 몇달전까지 비표준이였던 기술들이 표준이 되어버리는 것을 보고 공부를 하면서 프론트엔드가 정말 타 기술에 비해서 정말 빠르게 발전하고 있다는 것을 피부로 느낄 수 있었다.

- 또한 비표준에서 표준이 된 기술들을 하나같이 다 쓸모없는 것이 아니라 API와 라이브러리등 우리의 개발 생산성과 편리성을 높여주는 것들이라 더욱 앞으로의 기술의 발전이 기대된다. 기술의 발전하는 속도를 따라가기위해서 더욱 노력해야겠다.


<br></br>

___
___