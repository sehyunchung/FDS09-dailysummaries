#TIL_04_10_2조 정리  
## 유니코드 
문자를 **데이터베이스**화시킨 것
16진수 => XXXX(2**4)
4 bit = 16진수 한자리
8 bit = 1 byte
16 bit = 16 진수 네 자리 = 2 byte
### 정보의 표현(인코딩)
1. ASCII: 1 byte로 표현, 영어위주
2. UTF-8: 1 byte 는 영어 / 2 byte는 다른 언어 : 효율적인 저장 가능
3. UTF-16: 2 byte로 표현, 영어 이외 다른 나라 언어
### 문자열 리터럴

```js
'hello'
"hello 안녕하세요"
`hello world` // template literal
```

#### template Literal

- ES2015부터 나온 방식 .
- `(backtick)으로 문자열을 나타낸다.


- 문자열을 동적으로 생성하는 코드를 쉽게 작성 가능

```js
const sentence = `${name1} meets ${name2}!`;
```

- 여러줄로 이루어진 문자열을 쉽게 표현 가능

```js
`hello
world
hello
javascript!
`
```

#### escape sequence

```js
console.log('lorem \'ipsum\''); // lorem 'ipsum'
console.log('line\nfeed'); // line(줄바꿈)feed
console.log('\uD55C\uAE00'); // 한글
console.log('\u{1F435}'); // 🐵
```

- `\n`라인 피드(line feed)와 `\r`캐리지 리턴(carage return)은 **개행 문자**로,  우리가 보통 엔터를 누를 때 입력되는 문자  
- mac과 linux에서는 LF, windows에서는 CR+LF

### 문자열 과 연산자

```js
//유니코드 코드포인트 비교. 앞에서부터 한 글자씩 차례대로 비교합니다.
'aaa' < 'abc'; // true
'a' < 'Z'; // false

// 문자열을 배열로 바꾸기
let arr = [...'hello'];
console.log(arr);

//사전순 비교
'b'.localeCompare('a'); // 1
'b'.localeCompare('b'); // 0
'b'.localeCompare('z'); // -1
```
### 속성 및 메소드

```js
// 문자열의 길이 알아내기
'hello'.length; // 5

// 여러 문자열 연결하기
'hello'.concat('fun', 'javascript'); // 'hellofunjavascript'

// 특정 문자열을 반복하는 새 문자열 생성하기
'*'.repeat(3); // '***'

'hello javascript'.includes('hello'); // true
//hello가 문자열에 포함되어있는지
'hello javascript'.startsWith('he'); // true
'hello javascript'.endsWith('ript'); // true
//문자열이 he로 시작하는지 ript로 끝나는지
'hello javascript'.search('java'); // 6
'hello javascript'[6] 			  // 6
//java문자열이 시작하는 위치 반환
//문자열이 없으면 -1이 반환
```
## 삼항연산자 

조건에 따라 두 식 중 하나를 반환합니다.   
*if-else 문과 같은 조건문 방식(*true 혹은 false로 평가*)으로 작동함*
```javascript
// 삼항 연산자 (ternary operator)
true ? 1 : 2; // 1
false ? 1 : 2; // 2
// 조건 ? 조건이 ture일때 반환할 값 : 조건이 false일때 반환할 값
```
* '' 빈 문자열은 Falsy vs 빈 객체, 배열은 **Falsy아님**
##  연산자 우선순위.   
```javascript
true || true && false; // true
(true || true) && false; // false
true || false && false; // true
(true || false) && false; // false
// &&은 수식의 *(곱셈)처럼 작동한다.
//위 첫번째줄 예제에서는 true && false먼저 연산한 후 그 값을 true || 로 연산하는 순서로 작동
//그러므로 여러 연산자를 섞어 쓸 경우 괄호를 사용하는것이 좋다.
```


## truthy & falsy.  
JavaScript에서는 boolean 타입이 와야 하는 자리에 다른 타입의 값이 와도 에러가 나지 않고 실행됩니다.       
```javascript
if (1) {
  console.log('이 코드는 실행됩니다.');
}
if (0) {
  console.log('이 코드는 실행되지 않습니다.');
}
//이 예제에서 1이 truthy, 0이 falsy. 
```
이렇게 어떤 값들은 `true`로, 어떤 값들은 `false`로 취급되는데, 전자를 **truthy**, 후자를 **falsy**라고 부릅니다.    
 **JavaScript에서는 아래의 값들은 모두 falsy.  
- `false`
- `null`
- `undefined`
- `0`
- `NaN`
- `''`
  위의 6가지를 제외한 모든 값들은 truthy입니다.


## 다른 타입의 값을 진리값으로 변환하기   
어떤 값을 명시적으로 boolean 타입으로 변환해야 할 때가 있는데, 그 때에는 두 가지 방법을 사용할 수 있습니다.   
```javascript
!!'hello'; // true
Boolean('hello'); // true
//'hello'는 빈 값(0)이 아니라 값이 있으므로 true를 출력한다.
```

부정 연산자(`!`) 뒤의 값이 truthy이면 `false`, falsy이면 `true`를 반환하는 성질을 이용해서 이중 부정을 통해 값을 boolean 타입으로 변환할 수 있습니다.     <br><br>
> 1. `!`은 여집합, `||`는 합집합, `&&`는 교집합, `true`는 전체집합, `false`는 공집합으로 생각하면 됨.


## null과 undefined    
JavaScript에서   **'없음'를 나타내는 값** 2가지가 있다.
 `null`와 `undefined`입니다. 두 값의 의미는 비슷하지만, 각각이 사용되는 목적과 장소가 다르다. 
    
-  `undefined`   
> 값을 할당하지 않은 변수를 의미.     
> - `null`    
>   Computer science에서 `null`은 의도적으로 기본형(primitives) 또는 **object형 변수에 값이 없다**는 것을 명시한 것이다.    

만약, 프로그램에서 사용자가 입력한 값이 null인지 확인하고 싶을 때   
>`!=`  or  `==`  두 가지 방식 중 하나를 사용하여 확인한다.   
>그 외의 경우에는  `===` 사용하는것이 좋다.
><br><br>
#### 비교연산자 `==` & `===`
```javascript
const x = 5   
x == 5    //true    
x == '5'  //true   
x === '5' //false
// == 는 동등비교 : 형변환 후, 비교한다
// === 는 일치비교 : 값의 타입까지 일치해야 true 반환
```



## 정렬 알고리즘

- Bubble Sort
- Heap Sort
- Quick sort
- Selection sort
  [정렬 알고리즘][https://namu.wiki/w/%EC%A0%95%EB%A0%AC%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98]


## 객체(Object)
객체   
 = `{}` 속성을 저장하는 통.   -> 속성은 이름: 값 으로 표현.
```javascript
count obj = {a: 1, b: 2};
console.log(obj.a) //1 
console.log(obj['a'])//1
```
> 위 예제와 같이 객체의 프로퍼티에 접근하는 방법은 마침표(.) 표기법과 대괄호([]) 표기법이 있다.
* 객체의 속성 값에 접근하는 3가지 방법
```js
const obj = {a: 1, b:2}
```
> 1. obj.a;
>
> 2. obj['a'];
>
> 3. const x = 'a';
>    obj[x] = 1;  *중요