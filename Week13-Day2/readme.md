# 6/12 (화)

## 1. Today I learned

### 1-1. React 실습

#### 1-1-1. 카운터 만들기 실습

- 폴더 생성

```jsx
npx create-react-app fds-counter
```

- 먼저, 보여지는 부분부터 만들기

```jsx
class Counter extends Components {
  render(){
    const {number} = this.props;
     return(
      <div>
        <span>{number}</span>
        <button>증가</button>
      </div>
     )   
  }
}
```

- 상태만들기
  - App component
  - **상태를 바꾸는 함수**는 상태가 있는 컴포넌트에 있어야 한다.

```jsx
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  state = {
    number: 0
  }
  
 
  // 상태를 바꾸는 함수 (증가 시키는 함수)는 상태가 있는 컴포넌트에 만들어야한다.
  incNumber = () => {
    this.setState({
      number : this.state.number + 1
    });
    // this.state.number++; 는 화면을 다시 그리지 않는다.
  }

  render() {
    return (
      <div className="App">
        <Counter num={this.state.number} onIncClick={this.incNumber}/>
      </div>
    );
  }
}
// this.props 객체이고 객체의 속성이 됨
class Counter extends Component {
  render(){()
    const {num} = this.props;  //props는 읽기 전용이다. (값을 변경할 수 없다.)
     return(
      <div>
        <span>{num}</span>
        <button onClick={this.props.onIncClick}>증가</button>
      </div>
     )   
  }
}


export default App;
```



#### 1-1-2. 클릭하면 X 표가 생기는 10개의 상자

- 배열의 길이와 순서가 바뀌지 않는 경우에는 key값으로 index를 써주어도 된다.

```jsx
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  state = {
    checks : [
      false,
      false,
      false,
      false,
      false,
      false,
      false,
      false,
      false,
      false
    ]
  }
  handleCheck = index => {
    this.setState({
      checks : this.state.checks.map((check, i) => i === index ? true : check)
    })
  }
  render() {
    return (
      <div>
        {this.state.checks.map((check, index) =>
          <div key={index} className="box" 
              onClick={e => this.handleCheck(index)}>{check ? 'X' : 'O'}</div>
        )}
      </div>
    );
  }
}

export default App;

```



#### 1-1-3.  입력하는 숫자 더하기

- 제어되는 컴포넌트는 value와 onChange를 이용한다. 

```jsx
import React, { Component } from 'react';
//import logo from './logo.svg';
import './App.css';

class App extends Component {
  state = {
    number1: 3,
    number2: 4,
    result: 7
  }
  handleChangeNum1 = e => {
    this.setState({
      number1: e.target.value,
      result : parseInt(e.target.value) + parseInt(this.state.number2)
    });
  }
  handleChangeNum2 = e => {
    this.setState({
      number2: e.target.value,
      result : parseInt(e.target.value) + parseInt(this.state.number1)
    });
  }
  render() {
    return (
      <div>
        <input type="number" value={this.state.number1} onChange={this.handleChangeNum1} />
        <input type="number"  value={this.state.number2} onChange={this.handleChangeNum2} />
        <div>{this.state.result}</div>
      </div>
    );
  }
}

export default App;

```



- 다른 상태로부터 불러올 수 있는 값은 상태에 두지 않아도 된다.
  - result를 상태에서 제거한 코드

```jsx
import React, { Component } from 'react';
//import logo from './logo.svg';
import './App.css';

class App extends Component {
  state = {
    number1: 3,
    number2: 4,
  }
  handleChangeNum1 = e => {
    this.setState({
      number1: e.target.value,
      result : parseInt(e.target.value) + parseInt(this.state.number2)
    });
  }
  handleChangeNum2 = e => {
    this.setState({
      number2: e.target.value,
      result : parseInt(e.target.value) + parseInt(this.state.number1)
    });
  }
  render() {
    const result = parseInt(this.state.number1) + parseInt(this.state.number2)
    return(
      <div>
        <input type="number" value={this.state.number1} onChange={this.handleChangeNum1} />
        <input type="number"  value={this.state.number2} onChange={this.handleChangeNum2} />
        <div>{result}</div>
      </div>
    );
  }
}

export default App;

```



#### 1-1-4. 메뉴 선택하기


```jsx
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  state = {
   // 변하는 데이터를 담는 통  
    menu: null 
  };

  render() {
    return (
      <div>
        <button onClick={e => this.setState({menu: '짜장면'})}>짜장면</button>
        <button onClick={e => this.setState({menu: '짬뽕'})}>짬뽕</button>
        <button onClick={e => this.setState({menu: '볶음밥'})}>볶음밥</button>
        <div>{this.state.menu && `${this.state.menu}을 선택하셨습니다.`}</div>
      </div>
    );
  }
}

export default App;
```



- state 를 끌어올리기한 코드

```jsx
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  state = {
    menus : ['짜장면', '짬뽕', '볶음밥', '쟁반짜장'],
    menu: null
  }

// 상태를 바꿔주는 함수를 만들어서 내려주고 위의 상태를 바꾼다.
  updateMenu = menu => {
    this.setState({
      menu: menu
    })
  } 
  render() {
    return (
      <div>
        <MenuSelector menus={this.state.menus} menu= {this.state.menu} onUpdateMenu={this.updateMenu} />
      </div>
    );
  }
}

class MenuSelector extends Component {

  render(){
    const {
      menus,
      menu,
      onUpdateMenu
    } = this.props;

    return(
      <div>
      {menus.map(item => (
        <button onClick={e => onUpdateMenu(item)}>{item}</button>
      ))}
      <div>{menu && `${menu}을 선택하셨습니다.`}</div>
     </div> 
    )
  }
}

export default App;
```





### 1-1-5. 할일 관리

- newToBody가 App 컴포넌트의 state에 있는 코드

```jsx
import React, { Component } from 'react';
import './App.css';

let count = 1;

class App extends Component {
  state = {
    todos: [
      {
        id: count++,
        body: 'React 공부',
        complete: false
      },
      {
        id: count++,
        body: 'Redux 공부',
        complete: false
      }
    ],
    newTodoBody: ''
  }

  handleBodyUpdate = e => {
    this.setState({
      newTodoBody: e.target.value
    })
  }

  handleNewTodo = e => {
    const newTodo = {
      id: count++,
      body: this.state.newTodoBody,
      complete: false
    };
    this.setState({
      todos: [
        ...this.state.todos,
        newTodo
      ],
      newTodoBody: ''
    });
  }

  render() {
    const {newTodoBody} = this.state;
    return (
      <div>
        <TodoForm newTodoBody={newTodoBody} onUpdate={this.handleBodyUpdate} onAdd={this.handleNewTodo} />
        <TodoList todos={this.state.todos} />
      </div>
    )
  }
}

class TodoForm extends Component {
  render() {
    const {newTodoBody, onUpdate, onAdd} = this.props;
    return (
      <div>
        <input type="text" value={newTodoBody} onChange={onUpdate} />
        <button onClick={onAdd}>추가</button>
      </div>
    )
  }
}

class TodoList extends Component {
  render() {
    const {todos} = this.props;
    return (
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>{todo.body}</li>
        ))}
      </ul>
    )
  }
}

export default App;
```



- newToBody가 TodoForm 컴포넌트의 state에 있는 코드
  - 상태가 하나의 컴포넌트에 있을 필요는 없다.  여러 컴포넌트에 퍼져 있을 수 있다.
  - 상태는 필요로 하는 곳 가까운데 두는 것이 편하다.
  - todos는 TodoLIst, TodoForm에서 필요로 하므로 App에 위치시킨다.

```jsx
import React, { Component } from 'react';
import './App.css';

let count = 1;

class App extends Component {
  state = {
    todos: [
      {
        id: count++,
        body: 'React 공부',
        complete: false
      },
      {
        id: count++,
        body: 'Redux 공부',
        complete: false
      }
    ]
  }

  handleNewTodo = newTodoBody => {
    const newTodo = {
      id: count++,
      body: newTodoBody,
      complete: false
    };
    this.setState({
      todos: [
        ...this.state.todos,
        newTodo
      ]
    });
  }

  render() {
    return (
      <div>
        <TodoForm onAdd={this.handleNewTodo} />
        <TodoList todos={this.state.todos} />
      </div>
    )
  }
}

class TodoForm extends Component {
  state = {
    newTodoBody: ''
  };

  handleInputChange = e => {
    this.setState({
      newTodoBody: e.target.value
    });
  }

  handleButtonClick = e => {
    this.props.onAdd(this.state.newTodoBody);
    this.setState({
      newTodoBody: ''
    });
  }

  render() {
    const {onAdd} = this.props;
    const {newTodoBody} = this.state;
    return (
      <div>
        <input type="text" value={newTodoBody} onChange={this.handleInputChange} />
        <button onClick={this.handleButtonClick}>추가</button>
      </div>
    )
  }
}

class TodoList extends Component {
  render() {
    const {todos} = this.props;
    return (
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>{todo.body}</li>
        ))}
      </ul>
    )
  }
}

export default App;
```



- 컴포넌트가 나뉘어 있을 때 서로에 대해 모르고 있는 것이 좋다. 

  - todoForm이 어떻게 만들어졌는지에 대해서 어떠한 가정도 하지 않는 것이 좋다.

  - e 이 이벤트 객체를 봤을 때 어떤 이벤트 리스너인지 알 수없다.
    
     ```jsx
      handleInputChange = newTodoBody => {
        this.setState({
          newTodoBody
        });
      }
     ```



#### 실습 Keyword
  - 상태 
  - 상태를 바꿔서 내려주기
  - 역할과 책임에 맞게 코딩을 해야한다.
    - 공유해야 하는 state만 상류에 둔다.



---



### 1-2. Ref와 DOM

+ Ref는 render메소드에서 생성된 DOM 노드 혹은 React엘리먼트 객체에 접근할 수 있는 방법을 제공한다.

> 강사님왈 DOM에 접근하기 위해 사용됨

+ 가끔은 props를 가지고 다시 렌더링을 해주는 거싱 아닌, 데이터 흐름 밖에서 자식을 명령형(textcontent, focus method ...)으로 변경해야 할 필요가 있다.
  + 명령형 : textContent를 직접 바꾸거나, appendChild, focus 메소를 호출하거나 하는 것

+ 그럴 때 Ref를 사용한다.

  

#### 언제 ref를 사용해야 하나요?

- Ref의 바람직한 사용 사례로 다음과 같은 것을 들 수 있다.
  - 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때(메소드를 호출해야 하기 때문에)
  - 명령형 애니메이션을 발동시킬 때
  - 서드파티 DOM 라이브러리를 통합할 때 (리액트로 만들어지지 않은 다른 라이브러리를 리액트 세계에 붙일 때)

  

#### Ref 생성하기

- Ref는 객체이다. 

```js
myRef = React.createRef();

render() {
  return <div ref={this.myRef} />;
}

const node = this.myRef.current;
// current dom객체가 된다(리액트 객체가 아니라)
```



#### Ref 사용하기

- ref를 다 연결해준다음에 current속성을 통해서 DOM 노드 객체를 가져올 수 있다. 
- class 컴포넌트로 부터 생성되는 인스턴스 그 인스턴스에 접근할 때도 사용할 수 있다. 
- ref의 값은 노드의 유형에 따라 달라집니다:

- HTML 엘리먼트에 ref 어트리뷰트가 사용되면, ref의 current 속성은 DOM 엘리먼트 객체를 가리킵니다.
- 클래스 컴포넌트에 ref 어트리뷰트가 사용되면, ref의 current 속성은 해당 컴포넌트로부터 생성된 인스턴스를 가리킵니다.
- 함수형 컴포넌트(state, lifecycle기능이 없음)는 인스턴스를 가질 수 없기 때문에 ref 어트리뷰트 역시 사용할 수 없습니다. 한 번 화면을 그리고 말기 때문에 인스턴스라고 할 게 없다. 

- 실무에서도 거의 dom element에 ref만 사용하게 된다.



#### 실습

- 화면이 처음 로딩될 때 input에 focus 되게 하기

```jsx
import React, { Component } from 'react';
import './App.css';

let count = 1;

class App extends Component {
  formRef = React.createRef();
  state = {
    todos: [
      {
        id: count++,
        body: 'React 공부',
        complete: false
      },
      {
        id: count++,
        body: 'Redux 공부',
        complete: false
      }
    ]
  }

  handleNewTodo = newTodoBody => {
    const newTodo = {
      id: count++,
      body: newTodoBody,
      complete: false
    };
    this.setState({
      todos: [
        ...this.state.todos,
        newTodo
      ]
    });
  }

  render() {
    return (
      <div>
        <TodoForm ref={this.formRef} onAdd={this.handleNewTodo} />
        <TodoList todos={this.state.todos} />
      </div>
    )
  }
  componentDidMount(){
    console.log(this.formRef.current);
  }
}

class TodoForm extends Component {
  inputRef = React.createRef();

  state = {
    newTodoBody: ''
  };
  
  handleInputChange = e => {
    this.setState({
      newTodoBody: e.target.value
    });
  }
  handleButtonClick = e => {
    this.props.onAdd(this.state.newTodoBody);
    this.setState({
      newTodoBody:''
    });
  }
  componentDidMount(){
    this.inputRef.current.focus();
  }
  render() {
    const {onAdd} = this.props;
    const {newTodoBody} = this.state;
    return (
      <div>
        <input ref={this.inputRef} type="text" value={newTodoBody} onChange={this.handleInputChange} />
        <button onClick={this.handleButtonClick}>추가</button>
      </div>
    )
  }
}

class TodoList extends Component {
  render() {
    const {todos} = this.props;
    return (
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>{todo.body}</li>
        ))}
      </ul>
    )
  }
}

export default App;
```



## 2. Today I found out

- 실습을 하면서 배우니까 좋았다.
- 오늘 배운 실습에 빨리 익숙해져야 겠다.





## 3. 오늘 읽은 자료

[강사님 예제 코드](https://gist.github.com/seungha-kim/9583b69b561310b80e813c6b7d02af92)

