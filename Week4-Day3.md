# 4/11(수)

## Today I learned

### 함수 function
재사용하기 위해 코드 묶음을 정리해 놓은 단위

함수 호출의 결과값으로 반환값(return value)을 갖는다. 반환되는 즉시 함수 실행이 끝난다. `return` 구문이 없으면 undefined를 반환한다.

#### 함수의 구성 요소
```js
// 이름: add
function add(x, y) { // 매개변수(parameter): x, y
  const result = x + y;
  return result // 반환값: retrun value
}

// 함수 호출(call)
add(2, 3); // 인수(argument): 2, 3
```
위에서 add라는 이름을 갖는 함수를 정의했다. 괄호 안의 x와 y를 x, y를 매개변수(parameter)라 하며, return 뒤에 오는 값을 반환값(return value)이라고 한다.함수를 정의했다면, 아래와 같이 함수 이름 뒤에 괄호를 붙여서 이 함수를 실행시킬 수 있다. 이를 함수의 호출(function call)이라고 한다.

여기서 괄호 안에 넘겨준 2, 3을 인수(argument)라고 부른다.

#### 실행 순서
구문은 기본적으로 쓰여진 순서대로 실행되지만 구문 안에서의 순서는 복잡하다. 
(예. for loop, while loop)

함수 호출 코드 역시 실행 흐름을 왔다갔다하게 한다. 

function 키워드를 만나면 함수코드를 만들기만하고 넘어간다(실행이 아니다.) 
함수 호출이 일어나면 실행흐름이 다시 사전에 정의된 함수코드로 넘어간다. 
값이 반환되면 다시 실행 흐름이 호출한 곳으로 돌아간다.(코드 실행이 이전 위치에서 재개된다.)

```js
console.log(1);
function func() {
  console.log(2);
}
console.log(3);
func();
console.log(4);
// 1 - 함수 정의
// 3
// 2 - 함수 호출
// 4 - 나머지 코드 실행
```
함수를 정의하는 것만으로는 함수 내부에 있는 코드가 실행되지 않는다. 
실행하려면 반드시 함수를 호출해야한다.

#### 매개변수와 인수
매개변수는 변수의 일종(`const`, `var`, `let` 키워드로 선언하는 변수와 비슷한 성질) 
단, 함수 호출시마다 새로 정의되고 인수가 매개변수에 대입된다.

```js
function reassign(x) {
  x = 2;
  return x;
}
const y = 1;
const result = reassign(y);

// 변수를 인수로 써서 함수를 호출한다는 것은 
// 변수를 넘긴다는 것일까? 그 변수의 값을 넘기는 것일까?

// **인수에 변수가 들어가더라도 변수를 넘기는 것이 아니라 변수의 값을 넘기는 것이다**
// 그렇기 때문에 함수 내부의 동작이 변수 y에 영향을 끼치지 못한다. 
// 변수가 넘어간다고 치면 재대입이 가능해지기 때문에 잘못 동작될 것이다.
// 표현식의 값이 인수로 넘어간다.
// reassign(y + 1)이라고 하면 y + 1 표현식이 계산된 값이 인수로 넘어가는 것

// 반환되는 x 역시 변수x가 반환되는 것이 아니라 변수 x의 값이 반환되는 것이다.
console.log(y); // 1
console.log(result); // 2
```

#### 반환값
return 구문은 함수의 반환값을 결정
- return 키워드 바로 다음에 오는 함수 호출의 결과값으로 반환
- 반환되는 즉시 함수 실행이 끝남(뒤의 코드는 실행되지 않음)
- return 뒤에 아무 값이 없거나, 아예 return 구문을 쓰지 않으면 undefined를 반환(즉, 반환값이 없는 함수는 없다. 명시적으로 반환값을 쓰지 않을경우 undefined라는 값을 반환)

```js
function noReturn(){
  console.log(1);
  console.log(2);
  console.log(3);
};
noReturn(); // undefined;
```

### 스코프 (Scope)
```
function add(x, y) { // 변수 `x`와 `y`가 정의됨
  return x + y;
}
add(2, 3);
console.log(x); // 에러!
​````
> ReferenceError: x is not defined
    at eval:6:13
    at eval
    at new Promise

위에 코드를 보면 x에서 referenceError가 발생한다. 이는 변수가 유효한 스코프를 넘었기 때문이다. 스코프는 특정 변수가 유효한 범위라고 한다. c언어 에서의 지역변수의 범위와 비슷하다.
위예제에서는 함수 스코프를 같는다.

#### 스코프 연쇄 (Scope Chain)

함수 내부 코드에서, 매개변수 혹은 그 함수 안에서 정의된 변수만 사용할 수 있는 것은 아니다.
```
const five = 5;
function add5(x) {
  return x + five; // 바깥 스코프의 `five` 변수에 접근
}
add5(3); // 8
```
위의 코드는 add5 함수의 return 구문에서 함수 바깥에 있는 변수 five의 값을 가져와 사용했다. 이는 심지어 함수가 여러 겹 중첩(nested)되어 있다고 하더라도 가능하다. **이렇게 여러 겹의 중첩이 된 스코프를 스코프 연쇄라고 한다.**

코드의 실행 흐름이 식별자에 도달하면, 먼저 그 식별자와 같은 이름을 갖는 변수를 현재 스코프에서 찾아보고, 변수가 존재하면 그것을 그대로 사용한다.

만약 현재 스코프에서 변수를 찾지 못하면 바로 바깥쪽 스코프에서 변수를 찾아본다. 있으면 사용하고 없으면 바깥쪽 스코프로 올라가서 다시 찾아보는, 이 과정이 되풀이된다. 이런 과정을 스코프 연쇄(scope chain)라 하고, 이 과정은 가장 바깥쪽에 있는 스코프를 만날 때까지 반복된다. 가장 바깥쪽 스코프까지 찾아봤는데도 같은 이름의 변수를 찾지 못하면, 그제서야 에러가 발생한다.

#### 변수 가리기 (Variable Shadowing)

단일 스코프에서는 같은 이름을 갖는 서로 다른 변수가 존재할 수 없다. 하지만 스코프 연쇄가 일어나면 이야기가 달라진다. 아래의 코드에서는 x라는 이름을 갖는 변수가 세 번 정의되었다.
```
const x = 3;

function add5(x) { // `x`라는 변수가 다시 정의됨
  function add(x, y) { // `x`라는 변수가 다시 정의됨
    return x + y;
  }
  return add(x, 5);
}

add5(x);
```

위와 같이, 바깥쪽 스코프에 존재하는 변수와 같은 이름을 같는 변수를 안쪽 스코프에서 재정의할 수 있다. 그렇게 되면 안쪽 스코프에서는 바깥쪽 스코프에 있는 이름이 무시된다. 이런 현상을 변수 가리기(variable shadowing)라고 한다.

#### 어휘적 스코핑 (Lexical Scoping)

​```js
function add5(x) {
  // --- add5의 스코프
  const five = 5;
  return add(x); // 여기서 호출되었다고 해도 add5의 스코프에서 변수를 찾지 않는다.
  // --- add5의 스코프
}

add5(3); // 8

function add(x) {
  // --- add의 스코프
  return five + x; // ReferenceError: five is not defined
  // --- add의 스코프
}
```

스코프는 코드가 작성된 구조에 의해 결정(정의된 곳에서 결정)되는 것이지, 함수 호출의 형태에 의해 결정되는 것이 아니다. 스코프는 코드가 작성된 구조에 의해 결정되는 성질이다. 위 코드를 동작시키려면, 아래와 같이 작성해야 한다.

```js
function add5(x) {
  const five = 5;
  // add5안의 변수를 쓰고 싶다면 바깥 스코프로 둬야함
  function add(x) {
    return five + x;
  }
  return add(x);
}
```

사실 스코프의 종류가 더 있다. 특히, let과 const로 선언된 변수는 함수 스코프가 아니라 조금 다른 종류의 스코프를 가진다. 

#### 값으로서의 함수

```js
function add(x, y) {
  return x + y;
}

const plus = add;
plus(1, 2); // 3
```

함수는 값이다. 값으로서 할 수 있는 일은 다 할 수 있다.
- 변수에 대입해서 호출한다거나
- 배열이나 객체의 값으로 넣거나
- 함수(값)를 다른 함수의 인수로 넘길 수 있고
- 함수에서 함수(값)를 반환할 수 있다.

1급 시민/일급 객체/일급 엔티티(First-Class Citizen): 값으로 사용되는 것들  
자바스크립트의 함수는 1급 시민이고 1급 시민인 함수를 줄여서 **1급 함수**라고 한다.  
(위의 값으로서 할 수 있는 일들을 하는 함수)
- 변수나 데이터 구조안에 담을 수 있다
- 파라미터로 전달 할 수 있다
- 반환값으로 사용할 수 있다
- 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다
- 동적으로 프로퍼티 할당이 가능하다
[자바스크립트의 함수는 일급 객체이다](https://ko.wikipedia.org/wiki/%EC%9D%BC%EA%B8%89_%EA%B0%9D%EC%B2%B4)


#### 익명함수 (Anonymous Function)

JavaScript에서 함수를 선언할 때 꼭 이름을 붙여주어야 하는 것은 아니다.
이름을 붙이지 않은 함수를 가지고 익명 함수(anonymous function), 혹은 함수 리터럴(function literal)이라고 한다.
- 이름을 붙이지 않은 함수는 바로 호출을 할 수 없기 때문에 변수에 담아서 호출한다
```js
            // 함수 리터럴
            // 익명 함수
            // (함수 값, 값으로서의 함수)
const add = function(x, y) {
  return x + y;
}
// 호출하기 위해서 변수에 담아야한다.
add(1, 2); // 3
```
익명함수는 함수를 만든 쪽이 아니라 다른 쪽에서 그 함수를 호출할 때 많이 사용 
- 대표적인 경우는 함수를 인수로 넘겨줄 때

예를 들어, 배열의 filter 메소드에 필터링할 조건을 표현하는 함수를 넘겨주면, filter 메소드쪽에서 배열 각 요소에 대해 함수를 호출한 뒤, true를 반환한 요소만을 필터링해서 반환한다.
```js
// 함수를 인수로 넘겨줄 때
[1, 2, 3, 4, 5].filter(function(x) {
  return x % 2 === 0;
}); // [2, 4]
```
또는 아래처럼 작성
```js
var isEven = function (x) {
  return x % 2 === 0;
}

[1, 2, 3, 4, 5].filter(isEven); // [2, 4]
```

#### 화살표 함수 (Arrow Function)

함수 정의를 위한 새로운 표기법(ES2015 도입)

```js
// 제일 기본적인 표기법
        // 매개변수 // 리턴값
const add = (x, y) => x + y;
add(2, 3)

// 아래 함수와 '거의 동일하게' 동작한다.
function add(x, y) {
  return x + y;
}
```
화살표 함수는 표기법이 간단하기 때문에 익명 함수를 다른 함수의 인수로 넘길때 주로 사용된다.
```js
// 익명함수를 다른 함수의 인수로 넘길때 주로 사용
[1, 2, 3, 4, 5].filter(x => x % 2 === 0);
```

`=>` 다음에 써 있는 걸 반환. 바로 반환하거나 화살표 뒤에 중괄호로 둘러싸서 코드 작성
```js
// 바로 반환시키지 않고 function 키워드를 통한 함수 정의처럼 여러 구문을 사용하려면 curly braces({...}) 로 둘러싸주어야 한다.
// `=>` 다음 부분을 중괄호로 둘러싸면, 명시적으로 `return` 하지 않는 한 아무것도 반환되지 않는다.
const add = (x, y) => {
  const result = x + y;
  // 명시적으로 리턴을 해줘야한다.
  return result;
}
```
매개변수가 하나밖에 없다면 매개변수 부분의 괄호를 쓰지 않아도 됨
```js
const negate = x => !x;

// 아래와 거의 동일하게 동작
function negate(x) {
  return !x;
}
```

함수와 화살표 함수는 표기법만 다른 것이 아니고 차이점이 있음.

### 제어구문
코드의 실행에 영향을 미치는 구문
#### 조건문 
##### if ... else 구문
```js
function roll() {
  return Math.ceil(Math.random() * 6); // 주사위
}

function game() {
  const result = roll();

  alert(`결과: ${result}`); // 템플릿 리터럴

  // if...else 구문
  if (result >= 4) {
    // 괄호 안의 조건을 만족하면, 즉 결과값이 true 이면
    // 이 영역의 코드가 실행된다.
    alert('당신이 이겼습니다!');
  } else {
    // 위 조건을 만족하지 않으면, 즉 결과값이 false 이면
    // 대신 이 영역의 코드가 실행된다.
    alert('당신이 졌습니다.');
  }
}

game();
```

- else가 필요없는 경우 else를 생략할 수 있다.
- 중괄호 내부에 들어있는 구문이 하나라면, 중괄호를 생략할 수 있다. <br/> (언제든 코드가 추가될 수도 있어서 중괄호를 써주는 편이 좋을 수 있다.)

```js
if (result === 6) alert('당신은 운이 좋군요');
```


- 3개 이상의 경우의 수를 if ... else로 표현하려면 if ... else를 **중첩**시키면된다.
- - if else 안에 if else를 넣거나
- - `else if`를 통해 조건을 더 넣어준다.
```js
if(조건) {
 // 구문
} else{
  if(조건) {
    // 구문
  } else {
    // 구문
  } 
}
// 위의 중첩을 아래와 같이 else의 중괄호를 생략한 형태로 쓸 수 있다.
if(조건) {
  // 구문
} else if(조건) {
  // 구문
} else {
  // 구문
}
```



##### switch 구문
- `switch` 뒤 괄호(())의 값이 `case` 바로 뒤의 값과 일치하면 콜론(:) 뒤의 코드 영역이 실행된다. <br/> 일치하는 값이 아무것도 없으면 `default` 코드 영역이 대신 실행

- 하나의 변수에 대해 많은 경우의 수(값이 나올)가 있는 경우 switch 구문을 사용하는 것이 더 나을 수 있다.
```js
function translateColor(english) {
  let result;
  switch (english) {
    case 'red':
      result = '빨강색';
      break;
    case 'blue':
      result = '파랑색';
      break;
    case 'purple':
      result = '보라색';
      break;
    case 'violet':
      result = '보라색';
      break;
    default:
      result = '일치하는 색깔이 없습니다.';
  }
  return result;
}
```

- 단, `case` 뒤에 오는 코드 영역 마지막에 `break`를 써주지 않으면, 코드의 실행 흐름이 다음 코드 영역으로 넘어간다. <br/> (break를 만나면 실행 흐름이 switch문 바깥으로 넘어간다.)

- `break`를 써줘야 의도대로 동작한다. <br/> 단, break를 안써주는 경우
```js
// ...위의 코드에서
case 'purple':
case 'violet': // OR랑 비슷한 (English가 purple 이거나 violet이면)
  result = '보라색'; 
  break;
// ...
```
> 결과가 둘 다 보라색이므로 인수에 다른 값(purple, violet)을 넣어서 동일한 결과를 반환할 때는 다음 case의 내부로 들어가는 성질을 이용할 수도 있다.

- `break` 대신 `return`을 써도 함수를 끝내버려서 실행흐름이 바깥으로 나오기 때문에 다음과 같이 써도 잘 동작한다.
```js
function translateColor(english) {
  switch (english) {
    case 'red': return '빨강색';
    case 'blue': return '파랑색';
    case 'purple':
    case 'violet': return '보라색';
    default: return '일치하는 색깔이 없습니다.';
  }
}
```

- switch 구문은 자주 쓰지는 않는데 나중에 리액트 할 때 좀 쓰는 부분 있음  

- case 뒤에 and나 or 연산을 쓰는 것은 의미가 없음
- - switch 괄호 안의 값과 case 뒤의 값이 같은지 비교하는 것이기 때문
- - 아래와 같은 트릭도 가능한데, if가 좀 더 직관적임
```js
function limit(min, max, input) {
  switch(true) {
    case min>input :
      console.log(min);
      break;
    case max<input :
      console.log(max);
      break;
    default :
      return input;
  }
}

limit(3,7,5);
```
#### 반복문
유사한 작업을 여러번 반복해야할 경우  
- 객체(또는 배열)에 저장된 데이터마다 반복적인 작업을 하고 싶다거나
- 많은 데이터에 대해 반복적인 작업을 하고 싶을 때
- 굉장히 많은 방법이 있다. (기초적인 반복문 외에도.)

##### while 구문
```js
let i = 0; // 초기값

while (i < 5) { // 괄호 안의 값이 'truthy'인 한 안쪽의 코드는 계속 실행
  console.log(`현재 i의 값: ${i}`);
  i++; // 이거 없으면 조건이 갱신 되지 않아서(항상 조건이 true이므로) 무한 루프 주의
}

console.log('루프가 종료되었습니다.');
```
- 조건이 항상 true로 되게 만들어서 발생하는 무한루프에 주의하자  
- 무한루프가 필요한 경우도 있다. ( 그럴때는 일부러 쓴다고...(???) )
- for과 거의 동일하게 동작하지만 for로 쓰기 어려운 반복문이 있을 경우 쓰기도 한다.

##### do ... while 구문
내부의 코드를 무조건 한번 실행시킨다. 최소 한번 실행시키고 싶은 경우에 사용한다.
```js
do {
  console.log('do...while!');
} while(false);
```

##### for 구문
```js
for(let i = 0; i < 5; i++) {
  console.log(`현재 i의 값: ${i}`);
}
console.log('루프가 종료되었습니다.');
```

##### 배열의 순회: traverse
배열의 요소를 차례대로 찾아서 무언가를 하는 것

```js
const arr = [1, 2, 3, 4, 5];
for (let i = 0; i < arr.length; i++) {
  console.log(`배열의 ${i + 1}번째 요소는 ${arr[i]}입니다.`);
}
```
- 배열을 순회하는 데 for 구문이 많이 사용되었으나, ES2015부터는 배열 순회에 forEach나 for...of 구문이 더 많이 쓰인다.
- 각각의 차이점, 장단점이 있어서 적절한 때에 구분해서 사용한다.

```js
const arr = [1, 2, 3, 4, 5];
arr.forEach((item, index) => {
  console.log(`배열의 ${index + 1} 번째 요소는 ${item} 입니다.`);
})
```
```js
const arr = [1, 2, 3, 4, 5];
for (let item of arr) {
  console.log(`현재 요소는 ${item} 입니다.`);
}
```

##### break, continue
- break: 루프를 도중에 멈출 때
```js
  alert('퀴즈를 시작합니다.');
  while (true) {
    const answer = prompt('빨강의 보색은 무엇일까요?');
    if (answer === '초록') {
      alert('정답입니다! 🎉');
      break; // 루프를 종료하고 다음 코드로 넘어감
    } else {
      alert('틀렸습니다! 다시 시도해보세요.');
    }
  }
  alert('퀴즈가 끝났습니다.');
```


- continue: 남은 코드를 건너뛰어버리고 다음 번 차례로 넘어가야할 때.  <br/>  루프를 종료하지 않으면서 다음으로 번 차례로 넘어갈 때.
```js
  for (let i = 1; i < 100; i++) {
    console.log(`현재 숫자는 ${i} 입니다.`);
    if (i % 7 !== 0) {
      continue; // 루프의 나머지 코드를 건너뜀
    }
    console.log(`${i}는 7의 배수입니다.`);
  }
```

##### return, throw
`return`과 `throw`는 나머지 코드를 건너뛰고 함수를 즉시 종료시킨다.  <br/> (이후의 코드들은 실행되지 않는다)


- return은 본인이 있는 함수 실행만 종료하지만 throw는 모든 함수의 동작을 종료한다.

- **throw**: 에러처리한다.
```js
function a() {
  function b() {
    throw new Error('???');
  }
  const result = b();
  console.log('!!!');
  return result;
}

a();
// Error: ???
//     at b:3:11
//     at a:5:16
//     at eval:10:1
//     at eval
```


- return은 
```js
function a() {
  function b() {
    return 1;
  }
  const result = b();
  console.log('!!!');
  return result;
}

a(); 
// !!!
// 1;
```


## 2. Today I found out
생각하는 순서대로 구조를 짜기 위해선 문법 오류라도 안나게 기본 문법을 확실하게 익혀둬야 겠다는 생각이 들었다.

자바스크립트는 어렵다 하지만 다른 언어들 보다 쉽다. 하지만 또 그렇지만은 않은거 같다. 알고리즘은 굉장히 빠른 계산능력이 요구된다. 다른사람들은 잘 따라가는것 같은데 나만 못 따라 가는것 같아서 걱정이다. 잘 할 수 있을 까 ㅠㅠ 얼른 내것으로 만들어야 겠다. 어렵다.

스코프 연쇄나 어휘적 스코핑 부분은 들을때는 이해한 것 같은데 막상 다시 보니 어렵다. 전역변수, 지역 변수 개념만 알고 있었는데 ES2015부터는 다양한 스코프가 있어서 다른 개념이 존재한다니까 기존에 알던 것과 섞여서 헷갈린다. 블록 스코프는 들어봤는데  또 다른 스코프가 있다고 해서 앞으로의 강의에서 잘 이해할 수 있을지 걱정된다. 예습하고 복습하는 걸 철저히 해야할 것 같다.

일급 객체라는 개념이 신기했다. 자바스크립트나 파이선 이전의 언어들에서는 함수가 일급 객체가 아닌 경우가 있다고 하는 것 같은데, 도대체 그 당시 사람들은 그걸 어떻게 해결했는지 감탄이 나온다. 또한 arrow function 이라던지 let과 const를 보면서 자바스크립트가 매우 빨리 변화하고 있다는 것을 알 수 있었다. 10년 뒤는에 자바스크립트로 만들어진 수퍼컴퓨터가 나오는 것은 아닐까 (큰 기대는 하지 않지만).



## 3. 오늘 읽은 자료 (혹은 참고할 링크, 생략해도 됨)

[Mac OS X에서 git의 한글 호환 오류 문제 해결하기](http://resoneit.blogspot.kr/2013/06/git.html)
[자바스크립트의 함수는 일급 객체이다](https://ko.wikipedia.org/wiki/%EC%9D%BC%EA%B8%89_%EA%B0%9D%EC%B2%B4)