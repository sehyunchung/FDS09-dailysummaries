# 1. Today I learned

# React

## 수업들어가기전 중간 프로젝트 리뷰

### Pure DOM API 썼을 때의 문제점

- '어떻게' 하고 싶은지만 적혀있기 때문에, '무엇'을 하고 싶은지가 한 눈에 들어오지 않는다.
- 템플릿만 보면 뭘 하겠다는 것인지 보이지 않는다(템플릿 + js 코드를 한거번에 봐야 정확히 의도가 보인다.)
- 한 파일에 코딩할 수 있으면 좋겠다.
- 역할과 책임(role & responsibility)이 하나도 분리되어 있지 않다.
- 페이지를 그리는 함수에 통신, 템플릿 로딩, 템플릿과 데이터를 합치기, dom 트리에 병합시키는 코드가 다 들어있었다. 페이지를 그리는 데 필요한 모든 일을 다 하는 함수를 만들게 되었다.
- 코드가 전부 들어있었다. (뭐 하나 조금만 고쳐도 페이지를 다시 그려야 했다.)
  페이지의 일부분이 변경되더라도, 우리의 프레임워크 아래에서는 전체를 다시 로딩하는 수밖에 없었다.
- 코딩을 하기에는 쉬웠다. (데이터베이스가 변경될 때마다 페이지 전체를 매번 다시 그려주었기 때문에.)
- 화면은 변하는데 url 은 안 변한다.

## React quick start

### hello react!

### JSX소개

JSX를 react와 함께 사용하면, UI가 실제로 어덯게 보일지 서술할 수 있다. JSX는 템플릿 언어처럼 보일수 있지만 (ejs랑 완전다름, 템플릿 언어랑도 다름) 다르다.

#### 왜 JSX인가

렌더링 로직이 다른 UI로직과 본질적으로 결합되어있다는 사실을 인정한다. (이방법이 좋지 않다는 언어들도 간혹있음) react는 별도의 파일에 마크업과 로직을 넣음

#### JSX에 표현식 담기

```js
const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
)
```

```js
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### > 다넣을 수 있다. 심지어객체다!!

jsx는 다 camelCase를 쓴다 다 js로 바뀌어야 되기 때문에

#### JSX 자식 정의



#### JSX 인젝션 공격 예방


#### JSX 객체 표현

> tag ㅡ쓰는 거 다 객체다
> 표현식 아무거나 넣을 수 있다
> class이름 별도의 attribute를 사용하는 것이다.

### 요소(element) 렌더링

> 강사님왈: 내 개발인생은 react전과 후로 나뉜다.

`const element = <h1>Hello, world</h1>;`

브라우저 DOM요소와 다르게 React요소는 순수한 객체다
(ex `Const imgEl = document.getElementId(img)`애는 src는 이미지 다운로드 하기 등등 여러가지 기능들을 가지고 있다. 하지만 react객체는 아무것도 없다)

#### DOM 에서 element 렌더링하기

react DOM에의 해 관리되는 모든 것이 이 요소 안에 들어가므로, 이걸 루트 DOM노드라고 부른다.
보통 react로 구축한 어플리케이션은 root하나만 둔다.

React요소를 루트 DOM노드에 렌더링하고 싶다면 ReactDOM.render()에 둘다 넘겨주면된다.

#### React는 필요한 부분만 렌더링함

우리의 경험상, '시간 경과에 따라 UI를 어떻게 변경할지'지를 생각하는 것이 아니라 '특정 순간에 UI가 어떻게 보여져야 할지'에 대해 생각하면, 수많은 종류의 버그를 없앨 수 있다.

### 컴포넌트와 props

컴포넌트를 통해 UI를 독립적이고 재사용 가능한 부분으로 분리하고, 각 부분을 독립적으로 생각할 수 있다.

jsx 에서 태그이름이 소문자로 시작하면 html 로 생각하여 뿌려줌 그렇기에
컴포넌트를 만들 때는 무조건 대문자로 써야된다

#### 컴포넌트 추출

#### Props 는 읽기 전용

모든 React컴포넌트는 props에 대해서는 **순수 함수** 처럼 동작해야 한다.

어플리케이션 UI는 동적이며 시간이 지남에 따라 변한다. 다음 섹션에서는 새로운 컨셉인 state를 소개한다. state는 react컴포넌트가 이 규칙을 어기지 않고 유저액션, 네트워크 응답, 기타 등등에 대한 응답으로 시간 경과에 따라 출력을 변경할 수 있게 한다.

>함수형 컴포넌트는 프록스를 받아서 리액트 앨리먼트를 반환해 주는것이다.

클래스 객체를 만들어내기위한 틀이고 속성을 지정해줄수 있었다.

class에 로컬 state추가하기

> 밖에서 컴포넌트를 렌더링할때준 date가아니고 컴포넌트안에서 사용해보겟음
> 위에서는 그렇게 사용했음

1. render() 메서드 내의 this.props.date 를 this.state.date 로 바꿉니다.

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

1. this.state 를 초기화 하는 클래스 생성자 를 추가합니다.

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

3. <Clock /> 요소에서 date prop을 삭제합니다.

```js
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

결과

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

### 클래스에 라이프사이클 메서드 추가하기

state를 바꾼다음에 랜더 메소드가 활용이 되게끔하는게 리액트에서 화면을 그려주는 것

* this.setState가 하는 일은
    1. state를 바꿔주고
    2. 2. 화면을 다시그린다

많은 컴포넌트를 가진 어플리케이션에서, 컴포넌트가 제거될 때 사용중이던 자원을 돌려놓는 작업은 아주 중요한 일입니다.

Clock 이 DOM에 최초로 렌더링 될 때 타이머를 설정 하려고 합니다. React에서 이를 "mounting" 이라고 부릅니다.

그리고 DOM에서 Clock 이 삭제되었을 때 타이머를 해제 하려고 합니다. React에서 이를 "unmounting" 이라고 부릅니다.

컴포넌트가 마운트 (mount) 되거나 언마운트 (unmount) 되는 시점에 코드를 실행하기 위해, 컴포넌트 클래스에 특별한 메서드를 선언할 수 있습니다.

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    //상태를 바꿈으로써 화면이 간접적으로 다시 그려지도록 해줌
    this.setState({
      date: new Date()
    });
  }
// 상태로부터 화면이 어떻게 그려져야하는지를 render메소드에 서술
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

+ 이제 시계는 매 초 깜빡입니다.
+ 어떤 작업을 했는 지와 메서드가 호출되는 순서를 간단히 요약해봅시다.
+ <Clock /> 이 ReactDOM.render() 에 전달될 때, React는 Clock 컴포넌트의 생성자 함수를 호출합니다. Clock이 현재 시각을 화면에 보여주어야 하기 때문에, 현재 시각을 포함하는 + this.state 객체를 초기화합니다. 이 state는 추후 업데이트됩니다.
+ React가 Clock 컴포넌트의 render() 메서드를 호출합니다. 이를 통해 React는 화면에 무엇을 보여줘야 하는지 알아냅니다. 그다음 React는 DOM을 갱신해서 Clock 의 렌더링 출력과 + 일치시킵니다.
+ Clock 출력이 DOM에 주입되었을 때, React는 componentDidMount() 라이프 훅을 호출합니다. 그 안에서 Clock 컴포넌트는 브라우저에게 컴포넌트의 tick() 메서드를 초당 한 번씩 + 호출하는 타이머를 설정하라고 명령합니다.
+ 브라우저에서 매 초마다 tick() 메서드를 호출합니다. 그 안에서 Clock 컴포넌트는 현재 시각을 갖고 있는 객체를 가지고 setState() 를 호출하여 UI 업데이트를 예약합니다. setState ()  호출 덕분에, React는 상태가 변경된 걸 알게 됐고, render() 메서드를 다시 한 번 호출해 화면에 무엇을 표시해야 할지 알 수 있습니다. 이번에는, render() 메서드 내의 this.state.date 가 달라지므로 바뀐 시간이 출력에 포함됩니다. React는 그에 따라 DOM을 업데이트합니다.
+ 만약 Clock 컴포넌트가 DOM에서 삭제된다면, React는 componentWillUnmount() 라이프사이클 훅을 호출하기 때문에 타이머가 멈춥니다.
+ ReactDOM.render 와 setState일때만 render 함수가 호출된다
+ React의 사고방식 : 중간고사때는 페이지 다시 그리는 함수(render)를 호출했었음. 화면을 어떻게 그려야 하는지를 일일이 코딩을 해주었었음 하지만 React는 화면이 바꾸면 다시 그려지도록 + 해놨음. 두가지 절차는 상태가 있고 상태가 어떻게 그려져야 하는지만을 설명해 놓은 다음에 상태를 바꿈으로써 화면을 바꿈
+ 프로그래밍에서 결합이란 단어는 굉장히 안좋은 단어이다

### State 바르게 사용하기

+ state를 직접 수정하지 않는다. 
+ state 업데이트는 비동기일 수 있다. 
  + 리액트는 성능을 위해 여러 setState() 호출을 한 번의 작업으로 묶어서 처리하는 경우가 있다.(1초에 60번만 새로 그려주면 된다)
  + this.props 및 this.state가 비동기로 업데이트 될 수 있기 때문에 다음 state를 계산할 때 이 값을 신뢰해서는 안 된다.
  + 다음 state를 계산하기 위해 이전 state를 가져와야 하는 경우가 있다. 
  + 하나의 함수에서 state를 여러번 업데이트를 하고 싶을 수 있다. => 객체가 아닌 함수를 받는 두 번째 형식의 setState()를 사용할 수 있다. 

```js
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment // 이전 상태를 this.state로 받는 것이 아니고, 인수로 preState를 주었다. // 
}));

// 함수가 나중에 실행되지만 this.state가 아니고(지금 state가 아니고) 업데이트가 된 상태를 prevState에 넘겨준다. 
// 이전상태로부터 새 상태를 만들어낼 때는 위와 같은 형식(콜백 형식)의 setState를 사용해야 한다. 

```
setState안에서 this.state를 쓰면 안된다. 

### state 업데이트는 병합된다.

```js
  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });
    // posts 만 바꾸고 싶으면 posts만 넣어주면된다.(병합 되기 때문에)

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
```
assign과 같은 식으로 동작, 객체를 병합한다. 

### 데이터는 아래로 흐릅니다. 

표시하고 싶은 정보는 state안에 들어있고(저장하고) 자식 컴포넌트에 넘겨줄 때는 props을 통해서 넘겨준다. 
state에 지정을 해주면 자식에게 내려오지 않는다. props로 넘겨준다.
정보는 아래쪽으로만 흐른다. 공용으로 써야 하는 정보는 상류에 둬야 한다.

[할일 목록을 간단하게 구현해본 예제입니다.](https://codepen.io/dbeat999/pen/oyxGeE)

### 이벤트 제어하기

#### 이벤트와 리액트에 관련된 대표적인 예

```js
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 콜백에서 `this`가 제대로 동작하게 만들려면 아래 바인딩을 꼭 해주어야 합니다.
    this.handleClick = this.handleClick.bind(this);
  }

//이벤트 리스너 등장!

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```


#### 위의 예시에서 포인트

1.  React 내에서도 이벤트 리스너라는 개념이 등장!

        - `addEventListener`가 아닌 JSX 태그안에 `onClick`과 같은 이벤트를 주는것!

2. `Component Tag` 와 `Html Tag`의 차이가 있다!

    - Component Tag는 우리가 만들고 지정하는 것! <stopWatch> ; 여기에 `onClick`과 같은 이벤트를 걸어도 효과가 나타나지 않음!

    - Html Tag는 원래 알고있는 것들(div, input); 개별 항목이 되기때문에 여기에 `onClick`과 같은 이벤트를 준다!

3. `this`와 같은 개념은 정말 헷갈린다.

    - 이벤트 리스너를 쓸때는 `.bind(this)` 를 해주어도 되고, `eventname () => {}` 같이 화살표 함수를 써주어도 된다!


4. 위의 예시의 흐름은 

    - render()라는 함수를 통해 무엇을 보여줄지 우선 정해지고
    
    - 세부적으로 이벤트리스너와 같은 것을 지정해준다!



# 2. Today I found out
+ react를 드디어 접하였다. 어떻게 보면 react를 사용하기 위해서 여지껏 달려왔었는데 이제 드디어 사용을 해보는 데 역시나 처음에는 쉽지가 않다 현충일을 계기로 좀더 다듬고 공부를 진행해 보도록해야겠다.

+ 전에 배웠던 개념들을 다시 복습하는 것이 중요할 것 같다. 잘 이해가 안간다. 

+  화룡정점, 사생결단, 너죽고 나죽고.....리액트 만든사람만나고 싶다..

+  모순1: 여차저차해서 대단하신 개발자들이 쉽게 쓸수있는 것을 내놓았는데...옛날에 자바스크립트 배웠으면 이미 머리 다 빠졌을듯..

+  모순2: 오늘 한 것은 밥상에 밥 한숟가락이라는 데 난 한강 가야겠다..
