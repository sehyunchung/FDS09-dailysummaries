TIL 04/20/금 4조 

# 함수형 프로그래밍 (OOP)
함수를 인수로 받는 함수, 또는 함수를 반환하는 함수를 일러 고차 함수(higher-order function)라고 한다. 


## 고차 함수 (Higher-order Function)    

- **함수를 인수로 받는 함수**, 또는 **함수를 반환하는 함수**를 일러 **고차 함수(higher-order function)**라고 한다.

- 함수를 인수로 받는 `Array`의 많은 메소드들(`forEach`, `map`, `reduce`, `filter`, `sort`, `every`, `some`, `find` 등)은 고차 함수다.   

  ```js
  [1, 2, 3].map(x => x * 2)
  //위의 예제와 같이. 다른 함수의 인수로 넘겨지는 함수를 콜백(callback)이라고 부르기도 한다.
  ```

## 클로저(Closure)

맥락에 따라 다른 의미로 사용된다. 
+ 바깥 스코프에 있는 변수를 가져다 사용하는 함수
+ 변수가 저장되는 저장소(숨겨져 있는 저장소)

```js
function func1(x) {
  // 여기서 반환되는 함수는 바깥 스코프에 있는 변수 `x`를 사용하고 있습니다.
  return function () {
    return x;
  }
}

const func2 = func1(1);

// `func1`의 실행은 끝났지만, `func2`를 통해서 변수 `x`를 사용할 수 있습니다.
console.log(func2()); // 1
```

```js
const arr = [];

for (let i = 0; i < 10; i++) {
  // 여기서 만들어진 함수는 바깥 스코프에 있는 변수 `i`를 사용하고 있습니다.
  arr.push(function() {
    return i;
  });
}

// for 루프의 실행은 끝났지만, 루프 안에서 만들어진 함수가 배열에 저장되어 있습니다.
// 배열 안에 들어있는 함수를 통해, 해당 함수가 만들어진 시점의 변수 `i`를 사용할 수 있습니다.
console.log(arr[2]()); // 2
console.log(arr[5]()); // 5
```

주로 함수의 인자로 함수를 넘겨주기 위해 많이 사용된다.

숨겨진 변수를 사용하고 싶을때 함수, 배열로 변수를 묶어서 외부에서 간접적으로

접근, 변경할수 있게 하는 방법

```js
function personFactory(initialAge) {
  let age = initialAge;
  return {
    getOlder() {
      age++;
    },
    getAge() {
      return age;
    }
  };
}
const person = personFactory(20);
person.getAge();
```

personFactory에서 getOlder, getAge말고는 age에 접근할 수 있는 방법이 없다.

이때 getOlder, getAge를 클로저라고 하고, 클로저의 특징으로 age에 접근을 제한 할수도 있다.

```js
const makeAdder = x => (y => x + y);
makeAdder(2)(3);
// 결과값이 함수임으로 이런 방식으로도 쓸수 있다.
```

## 화살표 함수와 고차 함수

화살표 함수 문법을 이용하면, 적은 양의 코드만 사용해서 고차 함수를 만들 수 있다.

```
const makeAdder = x => y => x + y;

const add2 = makeAdder(2);
add2(3); // 5
```

```
const makeCounter = (x = 1) => () => x++;

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

## 재귀 함수 (Recursive Function)

- 함수 내부에서 **자기 자신을 호출하는 함수**가 재귀 함수(recursive function)이다.   
- 메모리는 유한한다.
- 브라우저가 최대 가지고 있는 stack 공간이 정해져 있다.
- 함수를 한번 호출할 때 마다 stack에 쌓인다 -> 메모리의 효율성 문제는?

### 분할 정복

병합 정렬 - code

```js
const arr = [7,3,8,5,2,4,6,1]
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const slicer = Math.floor(arr.length / 2);
  const arr1 = mergeSort(arr.slice(0, slicer));
  console.log(`arr1: ${arr1}`);
  console.log('-------')
  const arr2 = mergeSort(arr.slice(slicer));
  console.log(`arr2: ${arr2}`);
  
  const newArr = [];
  for (let i = 0, j = 0; i < arr1.length || j < arr2.length; ) {
    if (arr1[i] === undefined || arr1[i] > arr2[j]) {
      newArr.push(arr2[j]);
      j++;
    } else {
      newArr.push(arr1[i]);
      i++;
    }
  }
  return newArr;
}
```

```js
  mergeSort(arr);
arr1: 7
-------
arr2: 3
arr1: 3,7
-------
arr1: 8
-------
arr2: 5
arr2: 5,8
arr1: 3,5,7,8
-------
arr1: 2
-------
arr2: 4
arr1: 2,4
-------
arr1: 6
-------
arr2: 1
arr2: 1,6
arr2: 1,2,4,6
=> [ 1, 2, 3, 4, 5, 6, 7, 8 ]
```

---

# 객체 더 알아보기 

## 데이터 속성의 부수속성 

**'데이터 속성(data property)'**에 대한 속성 기술자는 네 가지 속성을 갖습니다.

- `value`: 속성에 어떤 값이 저장되어 있는지를 나타냅니다.
- `writable`: 변경할 수 있는 속성인지를 나타냅니다.
- `enumerable`: 열거 가능한 속성인지를 나타냅니다.
- `configurable`: 부수속성을 변경하거나 속성을 삭제할 수 있는지를 나타냅니다.

속성을 불러왔는데 함수가 실행되게 하는 함수

## 객체의 속성 열거하기

객체의 속성을 **열거할 때**에 사용할 수 있는 방법

- `Object.keys` - **객체 자신의 속성** 중 **열거 가능한(enumerable) 속성**의 이름을 배열로 반환합니다.

- `Object.values` - **객체 자신의 속성** 중 **열거 가능한(enumerable) 속성**의 속성 값을 배열로 반환합니다.

- `Object.entries` - **객체 자신의 속성** 중 **열거 가능한(enumerable) 속성**의 이름과 값을 배열로 반환합니다.

- `Object.getOwnPropertyNames` - **객체 자신의 모든 속성**의 이름을 배열로 반환합니다. 열거 불가능한 속성도 포함합니다.

- `for...in` 구문 - **객체 자신의 속성**부터 상속받은 속성까지 포함

  상속받은 속성까지 포함하는 단점이 있어 `for ...of` 구문이나 `Object.keys`를 사용한다.

```js
const obj = {
  a:1,
  b:2,
  c:3
};

Object.keys(obj);
Object.values(obj);
Object.entries(obj);

for(let name of Object.keys(obj)){
  console.log(name);
}

Object.keys(obj).forEach(item => console.log(item));

for(const [name, value] of Object.entries(obj)){
  console.log([name, value]);
}
```



## 얕은 복사(Shallow Copy) & 깊은 복사(Deep Copy)

객체가 중첩되어 있다면, 내부에 있는 객체는 복제되지 않습니다. 이것을 **얕은 복사**라 하고 `Object.assign`을 통해 속성이 값이 복사될 때, 실제로 복사되는 것은 중첩된 객체라 아니라 그에 대한 **참조**이기 때문입니다

중첩된 자료구조까지 모두 복사하는 것을 가지고 **깊은 복사(deep copy)**라고 합니다



### Object.preventExtensions

JavaScript는 특정 객체에 더 이상 속성을 추가하지 못하도록 막아버리는 기능을 제공합니다.

| 메소드                     | 속성 추가 | 속성 읽기 | 속성 변경 | 속성 삭제 및 재정의 |
| -------------------------- | --------- | --------- | --------- | ------------------- |
| `Object.preventExtensions` | X         | O         | O         | O                   |
| `Object.seal`              | X         | O         | O         | X                   |
| `Object.freeze`            | X         | O         | X         | X                   |