
## JavaScript Object

---

## 객체

자바스크립트에서 객체는 단순히 ‘이름(key):값(value)’형태의 프로퍼티들을 저장하는 컨테이너로서,<br/>
컴퓨터 과학 분야에서 해시라는 자료구조와 상당히 유사합니다.<br/>
자바스크립트에서 기본타입은 하나의 값만을 가지는 데 비해, 참조 타입인 객체는 여러 개의 프로퍼티들을 포함할 수 있으며,<br/>
이러한 객체의 프로퍼티는 기본 타입의 값을 포함하거나, 다른 객체를 가리킬 수도 있습니다.<br/>
이러한 프로퍼티의 성질에 따라 객체의 프로퍼티는 함수로 포함할 수 있으며, 자바스크립트에서는 이러한 프로퍼티를 메서드라고 부릅니다.<br/>

<br/><br/>

## 객체 리터럴

객체 리터럴을 이용해서 객체를 생성할 수 있습니다.<br/>
중괄호 안에 직접 이름-값 쌍을 적어주면 됩니다.<br/>

```js
const moong2 = {
  name: "홍길동",
  age: 29,
  gender: "male",
  email: "abc123@gmail.com"
};
```

위의 moong2 라는 변수에 할당된 객체에는 4 개의 속성이 저장되었습니다.<br/>
위의 속성 이름은 영어로 되어있지만 한글을 사용할 수도 있습니다.<br/>
단, 한글을 사용할 경우 ''를 써서 문자열 표기를 적어줘야 합니다.<br/>
속성의 이름도 식별자처럼 허용되지 않는 문자를 사용할 수 없지만 사용할 경우 문자열 표기를 해줘야 합니다.<br/>
객체 리터럴을 이용해 속성을 지정할 때, 이미 정의된 변수의 이름을 그대로 속성으로 사용할 수도 있습니다.<br/>

```js
const moong2 = {
  name: "홍길동"
  age: 29
};
```

위 코드를 아래처럼 쓸 수도 있습니다.<br/>

```js
const name = "홍길동";

const moong2 = {
  name,
  age: 29
};
```

객체의 속성과 값이 동일한 경우에는 이렇게 쓰면 됩니다.<br/>
단, 브라우저에서 지원이 안될수도 있으니 주의해야합니다.<br/>

```js
let o = {
  a: a,
  b: b,
  c: c
};

// 이렇게 단축이 됩니다.
let o = { a, b, c };
```

또한 대괄호를 사용해서 다른 변수에 저장된 문자열을 그대로 속성의 이름으로 쓰는 것도 가능합니다.<br/>

```js
const propName = "age";

const moong2 = {
  [propName]: 29
};

moong2.age;
```

<br/><br/>

## 점 표기법, 대괄호 표기법

속성 접근자(property accessor)를 이용해 이미 생성된 객체의 속성을 지정해줄 수도 있습니다.<br/>

```js
const moong2 = {};

moong2.name = "홍길동";
moong2.age = 29;
moong2.gender = "male";
moong2.computerLanguage = ["javascript", "java"];
```

객체 리터럴을 이용해 빈 객체를 생성한 후 점 표기법을 통해 속성을 갱신하였습니다.<br/>
그러나, JS 에서는 식별자로 허용되지 않는 문자가 들어간 속성 이름을 사용해야 하는 경우에 반드시 대괄호 표기법을 사용해야 합니다.<br/>

```js
moong2.['재밌게 본 영화'] = "lala land";
```

위와 같은 경우가 아니라면 주로 점 표기법을 많이 사용합니다.<br/>

<br/><br/>

## 객체 다루기

속성 접근자, delete 연산자, in 연산자를 통해 객체에 대한 정보를 읽고 쓸수 있습니다.<br/>

```js
const moong2 = {
  name: "홍길동",
  age: 29,
  gender: "male"
};

// 속성 읽기
moong2.name; //  "홍길동"
moong2.age; //  29

// 속성 쓰기 - 이전 속성에 있던 값이 갱신됩니다.
moong2.age = "마음만은 25세";

// 새 속성 추가하기
moong2.nickname = "취준";
moong2.favoriteGame = "Battle Ground";

// 속성 삭제하기
delete moong2.age;

// 속성이 객체에 있는지 확인하기 - 여부를 확인하여 있으면 true, 없으면 false 반환
"name" in moong2; //  true
"email" in moong2; //  false
```

<br/><br/>

## 메소드(Method)

객체의 속성값으로 함수를 지정할 수도 있습니다.<br/>

```js
const moong2 = {
    react = function () {
        return 'smile'
    }
};

moong2.react(); //  'smile'
```

이처럼 어떤 객체의 속성으로 접근해서 사용하는 함수를 메소드라고 합니다.<br/>
객체 리터럴 안에서 특별한 표기법을 사용해 메소드를 정의할 수 있습니다.<br/>

```js
const moong2 = {
  react() {
    return "smile";
  }
};

moong2.react(); //  'smile'
```

객체 속성 값으로 함수명을 지정하여 사용할 수도 있습니다.<br/>

```js
function greet() {
  return "hello";
}

const person = {
  greet: greet
};

person.greet();
```

위의 코드는 아래와 같습니다.<br/>

```js
let greet = function() {
  return "hello";
};

const person = {
  greet: greet
};

person.greet();
```

<br/><br/>

## this

다른 함수들과 달리 메소드라는 특별한 이름을 사용하는 이유는 메소드가 다른 함수들과 다르게 특별취급되기 때문입니다.<br/>
this 를 사용하면 메소드 호출 시에 해당 메소드를 갖고 있는 객체에 접근할 수 있습니다.<br/>

```js
const moong2 = {
  name: "홍길동",
  age: 29,
  introduce() {
    return `안녕하세요 제 이름은 ${this.name}이에요! 나이는 ${this.age}살입니다.`;
  },
  recovery() {
    this.age--;
  }
};

moong2.introduce(); // '안녕하세요 제 이름은 홍길동 이에요! 나이는 29살입니다.'
moong2.recovery(); //  undefined
moong2.introduce(); // '안녕하세요 제 이름은 홍길동 이에요! 나이는 28살입니다.'
```

메소드를 사용하면, 데이터와, 그 데이터와 관련된 동작을 객체라는 하나의 단위로 묶어서 다룰 수 있습니다.<br/>
이 것이 함수대신 메소드를 사용하는 핵심적인 이유입니다.<br/>
다만 function 키워드를 통해 정의된 함수 내부의 this 키워드가 실제로 무엇을 가리킬 것인가는<br/>
메소드가 어떻게 정의되는가에 의해 결정되는 것이 아니라 어떻게 사용되는가에 의해 결정됩니다.<br/>

```js
function thischeck() {
  return `이 this는 ${this.name}함수를 가리킵니다.`;
}

const func1 = {
  name: "func1",
  thischeck
};

const func2 = {
  name: "func2",
  thischeck
};

func1.thischeck();
func2.thischeck();
```

이렇게 thischeck 라는 함수가 객체 외부에서 정의되었고, func1 과 func2 에서 재사용되었는데 불구하고 메소드가 잘 동작했습니다.<br/>
즉, 같은 함수임에도 어떤 객체의 메소드로 사용되었느냐에 따라 내부의 this 가 가리키는 객체가 달라질 수 있다는 것입니다.<br/>
다만, 화살표 함수는 this 키워드를 전혀 다르게 취급하기 때문에 위와 같은 방식으로는 메소드로 사용될 수 없습니다.<br/>
또한, function 키워드를 통해 정의된 메소드가 항상 위와 같은 방식으로 this 를 취급하는 것은 아닙니다.<br/>
특별한 방법을 통해 아예 this 를 우리가 원하는 객체로 바꿔버릴 수 있습니다.<br/>

```js
function favoriteFood() {
  console.log(`${this.name}님이 좋아하시는 음식은 ${this.menu}입니다.`);
}

const info = { name: "홍길동", menu: "초밥" };
const favoriteFoodForMoong2 = favoriteFood.bind(info);

favoriteFoodForMoong2();
```

## JavaScript Array

---

## 배열

배열은 JS 에 내장되어 있는 자료구조입니다.<br/>
배열은 객체의 일종이지만, 내부적으로 특별하게 취급되어 일반적인 객체들과는 다른 특징을 갖고 있습니다.<br/>

```js
typeof []; //  'object'
```

배열 안에 들어있는 값들을 요소(element) 혹은 항목(item)이라고 합니다.<br/>

```js
let arr = [1, 2, 3, 4, 5];
```

객체와 배열의 가장 큰 차이점은 배열의 각 요소 간에는 순서가 있다는 점입니다.<br/>
배열은 `Array` 생성자의 인스턴스여서 배열의 프로토타입으로 `Array.prototype` 객체가 지정되어 있습니다.<br/>

<br/><br/>

## 배열 생성하기 - 배열 리터럴

배열은 배열 리터럴을 통해서 생성하는 것이 가장 쉽습니다.<br/>

```js
const empty = []; // 빈 배열
const numbers = [1, 2, 3, 4, 5]; // 숫자가 들어간 배열
const strings = ["가", "나", "다", "라"]; // 문자열이 들어간 배열
const objects = [{ prop: 1 }, { prop: 2 }, { prop: 3 }]; // 객체가 들어있는 배열
const anything = [1, "가", { prop: 3 }, true]; // 다양한 타입의 값들이 들어간 배열
```

<br/><br/>

## 배열 생성하기 - Array 생성자

`Array` 생성자를 이용하여 배열을 생성할 수 있습니다.<br/>
`Array` 생성자는 주어지는 인수에 따라 두 가지 서로 다른 방식으로 동작을 합니다.<br/>

```
1. 수 타입의 인수가 하나 주어질 때는 항상 수 만큼의 길이를 갖는 비어있는 배열을 만들어 냅니다.<br/>
   만약 인수가 양의 정수가 아니라면 에러를 냅니다.<br/>
2. 이 외에 다른 모양으로 인수가 주어지면 그 인수들을 요소로 갖는 배열을 생성합니다.<br/>
```

```js
new Array(1); //  [<1 empty item>]
new Array(1000); //  [<1000 empty item>]

new Array(1, 2, 3); //  [1,2,3]
```

<br/><br/>

## 배열 생성하기 - Array.of

일관적이지 못한 생성자의 동작방식 때문에 ES2015 에서 `Array.of` 정적 메소드가 추가되었습니다.<br/>
이 메소드는 위의 2 번 방식으로만 동작합니다.<br/>
따라서 Array 생성자를 사용할 때에는 1 번 방식만 쓰고,<br/>
2 번 방식의 코드를 작성할 때는 생성자 대신 Array.of 정적 메소드를 사용하도록 합니다.<br/>

```js
new Array(1, 2, 3); // [1,2,3] : 생성자는 이런 방식으로는 사용하지 않도록 합니다.
Array.of(1, 2, 3); // [1,2,3] : 가급적 Array.of로 하도록 합니다.

// Array.of 정적 메소드는 인수가 하나이더라도 그 인수를 요소로 갖는 배열을 갖습니다.
Array.of(1); //  [1]

// 생성자는 이런 용도로만 사용하도록 합니다.
new Array(1000); //  [<1000 empty item>]
```

<br/><br/>

## 배열 생성하기 - Array.form

JS 에서는 유사 배열 객체와 iterable 이라는 개념이 있어서, 이에 해당되는 값들은 Array.form 정적 메소드를 이용하여 쉽게 변환될 수 있습니다.<br/>

```js
//  'string' 타입은 래퍼 객체를 통해 iterable로 다루어질 수 있습니다.
Array.form("hello"); // ["h","e","l","l","o"]
```

<br/><br/>

## 요소 읽기

배열의 각 요소는 인덱스를 이용해 읽어올 수 있습니다.<br/>
인덱스는 객체의 속성 이름과 비슷한 역활을 하지만, 0 이상의 정수만이 배열의 인덱스가 될 수 있습니다.<br/>
배열을 생성하면 배열 안에 들어있는 각 요소는 순서대로 0 부터 시작하는 인덱스를 갖게 됩니다.<br/>
대괄호 표기법에 인덱스를 사용함으로써 원하는 요소를 가져올 수 있습니다.<br/>

```js
const arr = ["one", "two", "three"];

arr[0]; //  'one'
arr[1]; //  'two'
arr[2]; //  'three'
arr[3]; //  undefined
```

인덱스는 0 부터 시작하는 것을 꼭 주의해야합니다.<br/>

<br/><br/>

## 요소 수정하기

객체와 마찬가지로 대괄호 표기법을 이용해서 요소를 수정할 수 있습니다.<br/>

```js
const arr = [0, 1, 3, 3, 4];
arr[2] = 2;
console.log(arr); //  [0,1,2,3,4];
```

한꺼번에 많은 요소를 같은 값으로 바꿔야 할 때는 `fill` 메소드를 사용하면 됩니다.<br/>

```js
const arr = [0, 1, 2, 3, 4];

// 전체를 0으로 채우기
arr.fill(0);
console.log(arr); //  [0.0.0.0.0];

// 인덱스 1과 4사이를 1로 채우기
arr.fill(1, 1, 4); //  배열의이름.fill(채울값, 시작위치(포함), 종료위치(미포함))
console.log(arr); // [0,1,1,1,0];
```

`Array` 생성자와 `fill` 메소드를 사용하면, 큰 배열을 만들고 값을 채워넣는 일을 쉽게 할 수 있습니다.<br/>

```js
new Array(1000); //  [<1000 empty item>]
new Array(1000).fill(5); //  [5,5,5,5,5...]
```

<br/><br/>

## 배열의 끝 부분에서 요소를 추가/제거하기

`push` 메소드와 `pop` 메소드를 사용하면 배열의 끝 부분에서 요소를 추가/제거할 수 있습니다.<br/>

```js
const arr = [];
arr.push("one"); //  1 (요소가 추가된 후의 배열의 길이를 반환함)
arr.push("two", "three"); // 3

console.log(arr); //  ['one', 'two', 'three']

// 배열의 요소 삭제하기

arr.pop(); // 'three' 삭제
arr.pop(); // 'two' 삭제
arr.pop(); // 'one' 삭제
arr.pop(); // undefined (더 이상 배열에서 요소가 남아있지 않으면 'undefined'를 반환합니다.)
```

<br/><br/>

## 배열의 시작 부분에서 요소를 추가/제거하기

반대로 `unshift`, `shift` 메소드를 사용하여 배열의 시작 부분에서 요소를 추가하거나 제거할 수 있습니다.<br/>

```js
const arr = [];
arr.unshift(1); //  1 (요소가 추가된 후의 배열의 길이를 반환함)
arr.unshift(2, 3); //  3

console.log(arr); //  [2,3,1]

// 배열의 요소 삭제하기
arr.shift(); //  2
arr.shift(); //  3
arr.shift(); //  1
arr.shift(); //  undefined (더 이상 배열에서 요소가 남아있지 않으면 'undefined'를 반환합니다.)
```

<br/><br/>

## 요소를 배열 중간에 삽입하기

`splice` 메소드를 사용하면 배열에 속해있는 연속된 여러 요소, 즉 배열의 일부분을 통째로 바꿔버릴 수 있습니다.<br/>

```js
let arr = [1, 2, 3, 4, 5];

// 인덱스 1부터 3개를 바꿔칩니다.
// splice 메소드는 바꿔치기를 통해 제거된 요소를 반환합니다.

arr.splice(1, 3, "one", "three", "four); // 배열의이름.splice(인덱스시작지점, 바꿀개수, 바꿀 값)
console.log(arr); // [1, 'one', 'three', 'four', 5]
```

splice 를 통해 반드시 같은 개수의 요소만 바꿀수 있는 것은 아닙니다.

```js
let arr = [1, 2, 3, 4, 5];

arr.splice(1, 3, "ㅇ");
console.log(arr); // [1,'o',5]
```

splice 의 뒤쪽 인수를 생각하면, 요소를 제거할 뿐 배열에 아무것도 삽입하지 않습니다.

```js
let arr = [1, 2, 3, 4, 5];

arr.splice(1, 3); //  [2,3,4]
console.log(arr); //  [1,5]
```

이렇게 splice 메소드를 배열의 중간 부분에 있는 요소를 바꾸거나 제거할 때 사용할 수 있습니다.<br/>

<br/><br/>

## 배열 뒤집기

배열의 `reverse` 메소드를 호출하면 해당 배열을 거꾸로 뒤집을수 있습니다.<br/>

```js
const arr = [1, 2, 3];

// 'reverse' 메소드는 'arr'을 뒤집은 후, 'arr'을 그대로 반환합니다.
arr.reverse(); //  [3,2,1]
console.log(arr); //  [3,2,1]
```

<br/><br/>

## 배열 정렬하기

배열의 `sort` 메소드를 통해 원하는 방식대로 배열을 정렬할 수 있습니다.<br/>

```js
const arr = [3, 1, 4, 5, 2];

// sort 메소드는 arr을 비교 함수에 따라 정렬한 뒤, arr을 그대로 반환합니다.
arr.sort((a, b) => a - b); // 오림차순 정렬 [1,2,3,4,5];
console.log(arr); //  [1,2,3,4,5]
```

`sort` 메소드의 인수에는 비교함수를 넘겨줘야 합니다.<br/>
비교 함수는 인수를 두 개 받아서, 아래의 조건에 따라 잘 정렬되도록 적절한 값을 반환해줘야 합니다.<br/>

---

<br/>

만약 어떤 두 값 `a`, `b`에 대해서 비교 함수 compare 를 compare(a, b) 와 같이 호출했을 때 :

* 음수를 반환하면, a 가 b 앞에 오도록 합니다. (오름차순)
* 0 을 반환하면, a 와 b 를 같은 순서로 오도록 합니다.
* 양수를 반환하면, b 가 a 앞에 오도록 합니다. (내림차순)

<br/>

---

<br/>

따라서, 어떤 배열을 정렬할 때에는 어떤 값을 기준으로 정렬할 지 생각한 다음, 정렬함수를 만들 때<br/>
오름차순으로 정렬할지, 내림차순으로 정렬할지 생각해보면 됩니다.<br/>
예를 들어, 문자열의 길이를 기준으로 내림차순 정렬을 하고 싶다면 이렇게 하면 됩니다.<br/>

```js
const names = ["moong2", "min_zzz", "jogoogod", "shinyerin"];
names.sort((x, y) => y.length - x.length); //  내림차순이니까 양수를 반환하기 위해 y를 앞에다가 둡니다.
console.log(names); //  [ 'shinyerin', 'jogoogod', 'min_zzz', 'moong2' ]
```

간혹 비교함수를 넘기지 않아도 정렬이 잘 되는 것처럼 보일 수 있습니다.

```js
const arr = [1, 3, 2, 5, 4];
arr.sort(); // [1, 2, 3, 4, 5]
```

하지만 비교 함수를 인수로 넘기지 않을 경우, sort 메소드는 먼저 요소를 전부 문자열로 변환한 후<br/>
유니코드 코드 포인트를 비교하는 방식으로 정렬을 합니다. (대문자보다 소문자가 크다고 계산하기에 오차가 발생할 수 있습니다.)<br/>
반드시 sort 함수를 사용할 때는 비교 함수를 사용하도록 합니다.<br/>

```js
[20, 3, 100].sort(); //  [100, 20, 3] : 큰 수부터 정렬하는 것이 아니라 수의 첫 수를 보고 1,2,3 순으로 정렬이 된 것입니다.
["abc", "DEF", "aBC"].sort(); //  ["DEF", "aBC", "abc"]

[20, 3, 100].sort((x, y) => x - y); //  [3, 20, 100];
["abc", "DEF", "aBC"].sort((x, y) => x.localeCompare(y)); //  ['abc','aBC','DEF']
```

<br/><br/>

## 배열의 길이

배열의 길이는 `length`속성을 통해 쉽게 확인할 수 있습니다.<br/>
배열의 길이가 변함에 따라, length 속성의 값도 자동으로 달라집니다.<br/>

```js
const arr = [];
console.log(arr.length); //  0

arr.push(1, 2, 3);
console.log(arr.length); //  3
```

length 속성에 값을 대입해서 배열의 길이를 늘렸다가 줄였다가 할 수 있지만 권장하지 않습니다.<br/>

```js
const arr = [];

// 배열의 길이 늘이기
arr.length = 10;
console.log(arr); //  [ <10 empty items> ]

// 배열의 길이 줄이기 (줄어든 만큼 뒷쪽에 있는 요소들은 버려집니다.)
arr.fill(1); //  [1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
arr.length = 2;
console.log(arr); //  [1,1]

//이런 코드처럼 왠만하면 하지 않는게 좋습니다. 
```

<br/><br/>

## 배열 순회하기

배열의 각 요소를 차례대로 돌면서 요소에 대한 작업을 가지고 순회(traverse)라고 합니다.<br/>
배열에 접근하는 방법으로는 여러가지가 있습니다.<br/>

<br/><br/>

## 배열 순회하기 - for

```js
const arr = [1, 2, 3];

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

전통적으로 많이 썼던 방식이지만 `forEach` 메소드와 `for...of` 구문이 추가되면서 잘 쓰지 않습니다.<br/>

<br/><br/>

## 배열 순회하기 - forEach 메소드

배열에 forEach 메소드를 사용하면, 배열의 각 요소에 대해 함수를 호출할 수 있습니다.<br/>

```js
const str = [1, 2, 3];

arr.forEach(item => {
  consoel.log(`현재 요소 ${item}에 대해 함수가 실행되고 있습니다.`);
});
```

forEach 메소드에 넘기는 함수에는 총 세 개의 인수가 들어옵니다.<br/>

1.  현재 순회중인 배열의 요소
2.  요소의 인덱스
3.  순회중인 배열

```js
const arr = [1, 2, 3];
arr.forEach((item, index, array) => {
  console.log(`현재 ${index + 1}번째 요소에 대해 함수가 실행되고 있습니다.`);
});
```

<br/><br/>

## 배열 순회하기 - for...of 구문

ES2015 에 도입된 `for...of` 구문은, 역시 ES2015 에 도입된 iterable 을 순회하기 위해 사용할 수 있습니다.<br/>
배열 역시 iterable 이므로, for...of 구문을 사용해 순회할 수 있습니다.<br/>

> iterable(순회가능한 객체) : Symbol.iterator 심볼을 속성으로 가지고 있고, 이터레이터 객체를 반환하는 객체를 뜻합니다.

```js
const arr = [1, 2, 3, 4, 5];

for (let item of arr) {
  console.log(item);
}

// for문안에 (const item of arr)에서 const는 루프가 종료되고 다음 루프로 넘어갈때 선언이 날아가기 때문에 const를 써도 괜찮습니다.
const arr = [1, 2, 3, 4, 5];

for (const item of arr) {
  console.log(item);
}
```

어떤 것을 쓰는 게 좋을까요?<br/>

<br/>
단순히 배열을 순회하기 위한 목적이라면 `for...of` 구문을 사용하는 것이 코드의 간결성이나 속도 측면에서 유리합니다.<br/>
다만, 배열을 순회하면서 배열의 인덱스가 필요한 경우에는 `for...of` 구문을 사용할 수 없습니다.<br/>
이 때에는 `forEach` 메소드를 사용하면 됩니다.(forEach는 item, index, array를 모두 인수로 받기 때문입니다)<br/>
코드의 실행속도가 중요할 경우에는 `for` 구문을 쓰는게 좋습니다.<br/>

<br/><br/>

## 배열로부터 새로운 값 생성

배열을 다루다보면 배열로부터 다른 배열, 혹은 다른 값을 계산해내야 하는 작업을 많이 하게 됩니다.<br/>
배열을 순회하는 것만으로도 이런 작업을 할 수 있지만, 배열에 내장된 메소드를 활용하면 훨씬 더 간결한 코드로 같은 작업을 할 수 있습니다.<br/>
아래 메소드들은 모두 원본 배열에 아무런 영향을 미치지 않습니다.<br/>

<br/><br/>

## 배열로부터 새로운 값 생성 - slice

`slice` 메소드는 배열의 일부분에 해당되는 새로운 배열을 반환합니다.<br/>

```js
const arr = [1, 2, 3, 4, 5];

// 인덱스 2부터 인덱스 4 사이의 요소들을 가지고 새로운 배열을 생성
const newArr = arr.slice(2, 4); //  [3,4]

// newArr을 조작해도, 원본에는 아무런 영향을 미치지 않습니다.
newArr[0] = 5;
console.log(newArr); //  [5,4]
consoel.log(arr); //  [1,2,3,4,5]
```

첫 번째 인수의 기본값은 0, 두 번째 인수의 기본값은 배열의 length 속성입니다.<br/>
즉, 인수 없이 호출하면 배열 전체가 복사됩니다.<br/>

```js
const arr2 = arr.slice(); //  [1,2,3,4,5];
```

다만, `slice`는 얕은 복사를 하므로 배열 안에 배열 또는 객체가 들어가 있을 경우에는 주의해야합니다.<br/>

> 얕은 복사란? 객체안에 객체가 들어가 있는 경우에 객체 내부의 객체를 완벽히 복사하지 못하고 참조만 하는 것입니다. (자세히는 나중에 공부하도록 하겠습니다.)

<br/><br/>

## 배열로부터 새로운 값 생성 - map

`map` 메소드는 배열의 각 요소에 함수를 적용해서, 그 반환값을 요소로 갖는 새로운 배열을 만듭니다.<br/>
`forEach`와 비슷해 보이지만, 새로운 배열을 만든다는 점이 다릅니다.<br/>
(forEach 는 배열의 순회만 하지 반환하지 않습니다.)<br/>

```js
const arr = [1, 2, 3, 4, 5];

// arr의 각 요소를 제곱한 값으로 새 배열을 만듭니다.
const newArr = arr.map(item => item ** 2);
console.log(newArr); //  [1,4,9,16,25]
```

map 역시 인수로 들어온 함수를 호출할 떄 세 개의 인수를 넘깁니다. 이는 forEach 와 같습니다.<br/>

```js
arr.map((item, index, array) => {
  return item * index;
}); //  [0,2,6,12,20]
```

<br/><br/>

## 배열로부터 새로운 값 생성 - concat

`concat` 메소드는 여러 배열을 연결해서 새 배열을 만들 떄 사용됩니다.<br/>

```js
const arr = [1, 2];

arr.concat([3, 4], [5, 6], [7, 8]); //  [1,2,3,4,5,6,7,8]
```

<br/><br/>

## 배열로부터 새로운 값 생성 - filter

`filter` 메소드를 통해 배열에서 원하는 요소만을 골라서 새로운 배열을 생성할 수 있습니다.<br/>
filter 메소드에는 진리값(boolean)을 반환하는 함수를 주어야 합니다.<br/>
filter 메소드는 함수의 연산을 통해 truthy 면 새로운 배열에 포함되고, flasy 면 새로운 배열에 포함시키지 않습니다.
이처럼 진리값을 반환하는 함수를 predicate 라고 합니다.<br/>

```js
const arr = [1, 2, 3, 4, 5];

// 짝수만 골라내기
arr.filter(item => item % 2 === 0); //  [2,4] : 요소의 값이 2로 나눈 나머지가 0이면 true, 아니면 false를 반환합니다.
```

filter 에 주어지는 함수 역시 `forEach`와 마찬가지로 (현재요소, 인덱스, 배열) 세인수를 받습니다.<br/>

<br/><br/>

## 배열로부터 새로운 값 생성 - join

`join` 메소드는 배열의 요소들을 문자열로 변환 후, 메소드에 주어진 구분자(separator)를 이용해 하나의 문자열로 결합하여 반환합니다.<br/>

```js
const arr = [1, 2, 3];

arr.join("&"); //  '1&2&3'
```

구분자를 넘기지 않을 경우 `,` 문자가 구분자로 사용됩니다.

```js
const arr = [1, 2, 3];

arr.join(); //  '1,2,3'
```

<br/><br/>

## 요소 찾기

`indexOf`와 `lastIndexOf` 메소드를 사용하면 특정 요소가 배열의 몇 번째에 위치하는 지를 알아낼 수 있습니다.<br/>
`indexOf`는 배열의 왼쪽부터, `lastIndexOf`는 오른쪽부터 검색해서 처음 만나는 요소의 인덱스를 반환합니다.<br/>
만약 일치하는 요소가 없을 경우, 두 메소드 모두 `-1`을 반환합니다.<br/>

```js
const arr = ["a", "b", "c", "d", "c"];

arr.indexOf("b"); //  1
arr.lastIndexOf("c"); //  2

arr.indexOf("o"); //  -1
arr.lastIndexOf("s"); //  -1
```

두 메소드 모두 두 번째 인수로 시작 인덱스를 받습니다. 시작 인덱스가 주어지면 해당 인덱스부터 검사를 합니다.<br/>

```js
const arr = ["가", "나", "다", "라", "마", "가"];

arr.indexOf("가", 2); //  5 : 시작인덱스가 2로 주어져서 2(다)부터 검사를 하여 가를 찾았습니다. 값이 5인 이유는 시작인덱스부터 새도 인덱스 값의 기준은 0이며 변하지 않습니다.
arr.lastIndexOf("다", 2); //  2 : 거꾸로 2(라)부터 검사를 하여 다를 찾았습니다. 값이 2인 이유는 lastIndexOf또한 인덱스 값의 기준은 0이기 때문입니다.
```

`find` 메소드와 `findIndex` 메소드를 사용하면 특정 조건을 만족하는 요소를 찾을 수 있습니다.<br/>
두 메소드 모두 predicate(진리값 반환하는 함수)를 이용해 왼쪽부터 검사해서 처음 만나는 요소를 찾습니다.<br/>
`find`는 요소 자체를 반환하며, `findIndex`는 요소의 인덱스를 반환한다는 차이점이 있습니다.<br/>
조건을 만족하지 못하면 `find` 는 `undefined` 를 `findIndex` 는 `-1` 을 반환합니다.<br/>
(원하는 조건을 만족하는 요소가 필요할 때는 find, 조건에 만족하는 모든 것을 원할때는 filter, 인덱스가 필요하면 findIndex 를 쓰도록 합니다.)<br/>

```js
const names = ["moong2", "min_zzz", "jogoogod", "shinyerin"];

names.find(item => item.length > 6); //  'min_zzz' : 조건에 만족하는 요소중 왼쪽부터 검사해서 처음 만나는 요소이기 때문!
names.findIndex(item => item.length > 6); //  1 : 조건에 만족하는 요소중 왼쪽부터 검사해서 처음 만나는 요소(min_zzz)의 인덱스를 반환

names.find(item => item.length > 12); //  undefined
names.findIndex(item => item.length < 1); //  -1
```

`forEach`와 마찬가지로, `find`와 `findIndex`에 주어지는 predicate 에는 (현재요소, 인덱스, 배열) 세 인수가 넘겨집니다.

<br/><br/>