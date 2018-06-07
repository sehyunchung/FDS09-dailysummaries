# 6/07 (목)

## 1. Today I learend

### REACT 실습을 위해 환경 세팅하기 

1. 로컬 탐색기에서 빈 파일 만들기

2. 터미널에서 해당 파일로 이동 후, 아래 내용을 적는다
    ```
    npm install -g create-react-app	
    npx create-react-app (file name)

    or 

    npx create-react-app (file name)

    cd (file name)
    npm start
    ```


3. 필요에 따라 해당 파일들을 제거한다.
	- .css 
	- js..()
	- index.js 에서 
	
		- `import ... from '...'`
		- `import ... from '...'`
		- `js....()`


### 리스트와 키

- 컴포넌트 여러 개를 렌더링 하기
  - 요소 목록을 만든 뒤에는 중괄호 `{}`를 사용하여 `JSX`에 포함 시키는 것이 가능함.

  ```js
  const numbers = [1, 2, 3, 4, 5];
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  ```

  - 전체 `listItems` 배열을 `<ul>` 요소 안에 삽입해서 DOM에 렌더링 해줄 수 있다. 

  ```js
  ReactDOM.render(
    <ul>{listItems}</ul>,
    document.getElementById('root')
  );
  ```

- 기본적인 목록 컴포넌트

  ```js
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      <li>{number}</li>
    );
    return (
      <ul>{listItems}</ul>
    );
  }

  const numbers = [1, 2, 3, 4, 5];
  ReactDOM.render(
    <NumberList numbers={numbers} />,
    document.getElementById('root')
  );
  ```

  - 이 코드를 실행하면, 목록의 각 항목에 키를 넣어야 한다는 경고가 표시된다. `키(key)`는 요소 목록를 만들 때 포함해야하는 특수한 문자열 속성이다.
  - 목록 데이터를 렌더링 할 때는 `key`라는 prop을 리액트가 받아야 정상적으로 렌더링을 시켜준다
  - map callback에서 반환하는 요소에는 `key`를 반드시 넣어주어야 하며, index값은 넣어주지 않는게 좋다.

  - [Index as a key is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)
  - [왜 키가 필요한가](http://reactjs-org-ko.netlify.com/docs/reconciliation.html#recursing-on-children)
  - 키는 React에게 힌트를 제공하지만 컴포넌트로 전달되지는 않습니다. (역주: 컴포넌트 안에서 this.props.key와 같이 가져와서 쓰는 것이 불가능) 만약 컴포넌트에 동일한 값이 필요하다면 명시적으로 다른 이름의 prop으로 전달하세요.


- **key element on REACT**

  `key 값`의 역할은 사용자가 어떤 이벤트 트리거를 작동시켰을 때, `어떤 부분`에서 이벤트 트리거가 작동을 했는지, 그리고 `어떤 부분`을 변경해야하는지 모르기 때문에 `연결`을 통해 알 수 있도록 해주는 것이 `key`의 역할이다.

  `key` 를 안주면 REACT 는 `배열의 가장 마지막 값`을 `제거 (혹은 변경 개발자가 지정해준 이벤트)`해버리고 나머지 요소를 `땡겨서 표기해줄 뿐`이다.

  배열 내에서 사용되는 `key`는 `형제 간에 고유`해야 한다

  `key` 값은 컴포넌트 안에서 호출해서 `값으로써 사용할 수 없다` 필요하다면 "key" 가 아닌 다른 프로퍼티로 선언하고 사용해라

### form
- inner state
- React state를 **“진리의 유일한 원천 (single source of truth)“**으로 만들어 두 세계를 결합할 수 있습니다. 이렇게 하면 사용자의 입력에 따라 폼에서 발생되는 일을 React 컴포넌트 측에서 제어하게 됩니다. 이런 방식으로, React에 의해 제어되는 input 폼 요소를 “제어되는 컴포넌트” 라고 부릅니다.

- **input 요소 제어하기** 


  ```js
  class NameForm extends React.Component {
    constructor(props) {
      super(props);
      this.state = {value: ''};

      this.handleChange = this.handleChange.bind(this);
      this.handleSubmit = this.handleSubmit.bind(this);
    }

    handleChange(event) {
      this.setState({value: event.target.value});
    }

    handleSubmit(event) {
      alert('A name was submitted: ' + this.state.value);
      event.preventDefault();
    }

    render() {
      return (
        <form onSubmit={this.handleSubmit}>
          <label>
            Name:
            // REACT 에서 input 요소에 value 값이 들어가 있으면, 새로운 값으로 수정하지 못하게 된다
            <input type="text" value={this.state.value} onChange={this.handleChange} />
          </label>
          <input type="submit" value="Submit" />
        </form>
      );
    }
  }
  ```


- 위의 코드 분석 

  - input 안에 `새로운 값이 들어올 때마다`, `onChange() 이벤트`가 발동

  - 새로 입력된 값이 계속해서 `handleChange() 컴포넌트에 의해` setState 매소드로 인해 `새로운 값이 계속해서 state 에 반영`되고 있다

  - 새로 바뀌고 있는 state에 의해 input 안에 `value 값이 역시 반영`되고 있고, 

  - 사용자는 state 값과는 별개로 입력하는 것이 그대로 input 안에 적히고 있는 것처럼 판단하게 된다

  - input 안에 원하는 조건을 넣기 위해서 ex. 글짜 수 제안, 모두 대문자 표기 등 `this.setState({value: event.target.value} value 조건을 변경`하면 된다

  - `value: event.target.value.toUpperCase()` etc..

  REACT 안에서는 <texterea /> 요소 안에서 `value` 속성을 사용할 수 있다

### select 태그

HTML에서, `<select>` 는 드롭 다운 목록을 만듭니다. 예를 들어, 이 HTML은 과일 드롭 다운 목록을 만듭니다.

```html
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>

```

Coconut 옵션에 `selected` 어트리뷰트가 있기 때문에 기본적으로 선택되는 걸 주목합시다. React에서는 `selected` 어트리뷰트를 사용하는 대신 `select` 태그에 `value` 어트리뷰트를 사용합니다. 제어되는 컴포넌트를 쓸 때는 이 방식이 더 편한데, 한 곳에서만 업데이트를 해주면 되기 때문입니다. 예를 들어 보겠습니다:

```js
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite La Croix flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

```

- **하나의 컴포넌트를 이용해 여러 입력 요소 제어하기** 

  ```js
  class Reservation extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        isGoing: true,
        numberOfGuests: 2,
        nameOfGuest: 'fds'
      };

      this.handleInputChange = this.handleInputChange.bind(this);
    }
    // 사용하는 기능이 동일하면 하나의 컴포넌트로 여러 제어 필드에 활용할 수 있지만, 제한 요구조건이 다르기 때문에 기능이 다른 컴포넌트가 필요하다면 따로 정의해줘야 한다
    handleInputChange(event) {
      const target = event.target;
      const value = target.type === 'checkbox' ? target.checked : target.value;
      const name = target.name;
      // 하나의 컴포넌트를 활용해서 여러 제어 필드에 활용하는 예제
      this.setState({
        [name]: value
      });
    }

    render() {
      return (
        <form>
          <label>
            Is going:
            <input
              name="isGoing"
              type="checkbox"
              checked={this.state.isGoing}
              onChange={this.handleInputChange} />
          </label>
          <br />
          <label>
            Number of guests:
            <input
              name="numberOfGuests"
              type="number"
              value={this.state.numberOfGuests}
              onChange={this.handleInputChange} />
          </label>
          <br />
          <label>
            Name:
            <input
              name="nameOfGuest"
              type="text"
              // value={null} 이 들어가도 작동하는 것 처럼 보일 수 있음. 유의!!
              // 따라서 오타가 나면 안 된다는 말 this.state.mame 동작함
              value={this.state.nameOfGuest}
              onChange={this.handleInputChange} />
          </label>
        </form>
      );
    }
  }

  ReactDOM.render(
    <Reservation />,
    document.getElementById('root')
  );

  ```


REACT 에서 표현식을 넘길 때는,

`text` 

- " text " 따옴표 안에 표기 가능
- {" text "} 중괄호 안에 따옴표와 함께 넣어서 표기 가능

`boolean` , `number`

- { } 중괄호 안에 넣어줄 것
- { null }, { 0 }, { true } ...

### State 끌어올리기 

끌어올리기 에서 가장 중요한 것은

`자식`이 `부모의 상태를 변경`하고 싶을 때는

1. 반드시 `부모의 상태를 변경하는 매소드`를 `props` 를 통해 `자식에게` 넘겨주고

2. 자식이 그 매소드를 호출 및 사용하여 값을 변경하면

3. `변경된 값`이 `부모의 상태까지 변경`하도록 해야한다

#### Single source of trueth 하나의 진리의 원천

REACT 에서 상태를 값에 대한 상태를 변경해야 하는 부분이 있다면,

`State 를 한 곳에서만` 변경/관리할 수 있도록 하는 것이 중요하다.

여기저기에서 값을 변경할 수 있도록 소스를 풀어주게 된다면, 관리 측면에서 어려움이 있을 수 있다.

하나의 진리 원천은 에러가 발생하는 부분을 찾는 것에 있어 수월할 수 있다.

### 제어되는 입력 필드의 Null 값

[제어되는 컴포넌트](http://reactjs-org-ko.netlify.com/docs/forms.html#controlled-components) 의 value prop 값을 지정해주면, 개발자가 직접 value prop을 변경하는 방법 외에는 사용자가 입력 필드의 값을 변경할 수 있는 방법이 없습니다. `value` 를 정의했지만 여전히 입력 필드가 수정 가능한 경우라면 실수로 `value` 를 `undefined` 나 `null` 로 설정했을 수 있습니다.

다음 코드는 위와 같은 상황을 보여줍니다. (처음 보이는 input은 잠겨있지만 약간의 시간이 지난 후 수정 가능하게 바뀝니다)

```
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);

```

### 제어되는 컴포넌트에 대한 대안책

제어되는 컴포넌트를 사용하는 일은 종종 따분할 수 있는데, 왜냐하면 데이터를 변경하는 모든 방법에 대한 이벤트 핸들러를 작성해야하고 또 하나의 React 컴포넌트에 모든 input state를 전달해야하기 때문입니다. 기존 코드베이스를 React로 변경하거나 React 어플리케이션을 React가 아닌 라이브러리와 통합할 때 이 작업은 성가신 작업일 수 있습니다. 이런 상황에서는 입력 폼을 구현하기 위한 대체 기술인 [제어되지 않는 컴포넌트](http://reactjs-org-ko.netlify.com/docs/uncontrolled-components.html) 를 확인해보세요.


## 2. Today I found out
- 늘 새로워,,,
- 배열 매소드에 대해 더 많이 공부해야 할 것 같다.
- 리엑트가 좋다고하는데 아직까지는 너무어렵다 복습의 필요성을 느낌 손에 익혀야할듯
- 리액트는 매우 효율적인 방법이지만 특성 때문에 익숙해 지기 매우 어려운 것 같다. 특히 스테이트는 강력한 기능이지만 이를 전달하는데 있어 이해하기 어려움을 갖는다. 확실히 익숙해지면 매우 효율적일 것 같으니 많은 연습이 필요하겠다. 그리고 벌써 스테이트의 관리가 힘든 것을 보아 리덕스가 꼭 필요할 것 같다.
- 새로운 것을 배우는것에 대한 흥미가 좀 더 생길 수 있는 무언가를 해야할거같다.