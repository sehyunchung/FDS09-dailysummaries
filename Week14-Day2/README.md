# 6/19 (화)

## 1. Today I learned

### 1-1. Provider의 적절한 위치 

- Uncaught (in promise) Error: Request failed with status code 401
  - 401 Error : 인증이 되지 않은 상태

- 문제점 : 로그인을 하지도 않았는데 GET 요청이 갔다.

  

##### TodoContext.js

- GET 요청을 보내는 코드를 찾는다.

```jsx
export class TodoProvider extends Component {
  state = {
    loading: false,
    todos: [
    ]
  }  
  async componentDidMount(){
    await this.fetchTodos(); //
  }
  fetchTodos = async () => {
    this.setState({
      loading: true
    })
    const res = await todoAPI.get('/todos')
    this.setState({
      todos: res.data,
      loading: false
    }) 
  }
```



##### App.js

- TodoProvider를 제거한다. 

```jsx
export default class App extends React.Component {
  render() {
    return (
      <PageProvider>
        <UserProvider>
          <TodoProvider> 
            <PageConsumer>
              {value => value.page === 'login' ? (
                <LoginPage />
              ) : (
                <TodoPage />
              )}
              
            </PageConsumer>
          </TodoProvider>
        </UserProvider>  
      </PageProvider>
    )
  }
}
```


##### TodoPage.js

- TodoProvider로  감싸준다.
  - 컴포넌트이면서 상태를 갖고 있으면서 외부세계와 연동되어있다.

```jsx
import React, { Component } from 'react';
import TodoContainer from '../containers/TodoContainer';

export default class TodoPage extends Component {
  render() {
    return (
      <TodoProvider>   
        <TodoContainer />
      </TodoProvider> 
    );
  }
}

```



#### rendering 

- **rendering된다는 것은 화면을 그린다는 것이 아니다** 

- 컴포넌트 클래스로부터 생성되는 객체가 있다. 
- 컴포넌트 렌더링 = 컴포넌트의 인스턴스 트리 구축 
- 새 트리를 만들어보고 예전 트리와 일치하면 객체를 유지시키고, 일치하지 않는 부분은 객체를 날려버린다. 그 객체 안에 있던 정보도 날아간다. 



#### 로그아웃 버튼 만들기

- 로그아웃 기능 
  - 토큰을 지운다.  
  - 페이지를 바꾼다.

##### UserContext.js

- 토큰을 지운다.

```jsx
class UserProvider extends React.Component {
  login = async (username, password) => {
    try {
      // 로그인 요청
      const res = await todoAPI.post('/users/login',{
        username : username,
        password: password
      })
        // localStorage에 토큰 저장
        localStorage.setItem('token', res.data.token);
    } catch(e) {
      if(e.response && e.response.status === 400) {
          alert('아이디 혹은 비밀번호가 일치하지 않습니다.');
      }
    }
  }
  // 로그아웃은 동기식
  logout = () => {
    localStorage.removeItem('token')
  }

  render(){
    const value = {
      login: this.login,
      logout: this.logout
    }
    return (
      <Provider value={value}>{this.props.children}</Provider>
    )
  }
}
```



##### PageContext.js

- 페이지를 변경한다.

```jsx
import React from 'react';

const {Provider, Consumer} = React.createContext();

class PageProvider extends React.Component {
  state = {
    page: 'login'
  }

  goToTodoPage = () => {
    this.setState({
      page: 'todo'
    });
  }
  
  goToLoginPage = () => {
    this.setState({
      page: 'login'
    });
  }
  
  render(){
    const value = {
      page: this.state.page,
      goToTodoPage: this.goToTodoPage,
      goToLoginPage: this.goToLoginPage
    }
    return (
      <Provider value={value}>
        {this.props.children}
      </Provider>
    )
  }
}

export {PageProvider, Consumer as PageConsumer};
```



##### LogoutButtonContainer.js  파일 생성

```jsx
import React from 'react';
import {UserConsumer} from '../contexts/UserContext';
import {PageConsumer} from '../contexts/PageContext'

export default class LogoutButtonContainer extends React.Component {
  render(){
    return (
      <UserConsumer>
        {({loginout}) =>(
          <PageConsumer>
          {({goToLoginPage}) => (
            <button onClick={e => {
              logout();
              goToLoginPage();
            }}>로그아웃</button>
           }}/>
          )}
          </PageConsumer>
        )}
      </UserConsumer>
    )
  }
}
```



##### TodoPage.js 

- LogoutButtonContainer 추가

```jsx
import React, { Component } from 'react';
import TodoContainer from '../containers/TodoContainer';
import {TodoProvider} from './contexts/TodoContext';
import LogoutButtonContainer from '../containers/LogoutButtonContainer';
export default class TodoPage extends Component {
  render() {
    return (
      <TodoProvider>   
        <TodoContainer />
        <LogoutButtonContainer />
      </TodoProvider> 
    );
  }
}

```

- 과제 :  App.js에 TodoProvider 옮기는 연습 해보기 (어떤 차이가 생기는지 생각하기)

  

---



### 1-2. OnMount 컴포넌트

#### mount되었을 때 부작용을 일으키는 component

- 부작용이란? 
  - 상태를 바꾸거나 외부세계에 영향을 주는 것 
- 부작용을 활용해서 기능을 구현한다. 
- component를 렌더링하다는 것이 화면을 그린다는 것이 전부가 아니다.
- 화면과는 상관없이 부작용을 일으키기 위해서 컴포넌트를 렌더링하기도 한다.

```jsx
  async componentDidMount(){
    await this.fetchTodos();
  }
// 통신을 하고, 상태를 바꾸는 부작용이 있다.
```



- 문제점 : 로그인을 하고 새로 고침을 하면 다시 LoginPage로 간다.
  - 토큰이 저장되어있으면 TodoPage, 토큰이 없으면 LoginPage 를 보여주기

    

####  1-2-1. App.js에 OnMount가 있는 경우

##### App.js

```jsx
  import React from 'react';
  import TodoPage from './pages/TodoPage';
  import LoginPage from './pages/LoginPage';

  import {PageProvider, PageConsumer} from './contexts/PageContext';
  import {UserProvider} from './contexts/UserContext';
  import OnMount from './components/OnMount'

  export default class App extends React.Component {
    render() {
      return (
        <PageProvider>
          <UserProvider>
            <PageConsumer>
              {value => value.page === 'todo' ? (
                <TodoPage />
              ) : ( 
                <LoginPage />
              )} 
            </PageConsumer>
            <PageConsumer>
              {value => (
                localStorage.getItem('token') && <OnMount onMount={value.goToTodoPage} />
              )} 
                {/* 
                토큰이 undefined 가 나오면 렌더링이 되지 않는다.
                토큰이 있으면 OnMount가 렌더링이 되어서 mount되는 순간에 goToTodoPage가 실행된다.
                PageProvider의 상태가 바뀌고 밑부분이 다시 렌더링된다.
                */}
            </PageConsumer>
          </UserProvider>  
        </PageProvider>
      )
    }
  }
```

##### OnMount.js 생성

- 렌더링 했을 때 함수를 실행시키기 위해서 쓴다.

```jsx
import React from 'react';

export default class OnMount extends React.Component {
  componentDidMount(){
    const{onMount} = this.props;
    onMount();
  }
  render() {
    return null;
  }
}
```





#### 1-2-2. App.js 의 OnMount 코드를 LoginFormContianer.js로 옮기기 

##### LoginFormContianer.js

```jsx
import React from 'react';
import LoginForm from '../components/LoginForm';
import {UserConsumer} from '../contexts/UserContext';
import {PageConsumer} from '../contexts/PageContext';
import OnMount from '../components/OnMount';
export default class LoginFormContainer extends React.Component {
  render(){
    return (
      <UserConsumer>
        {({login}) =>(
          <PageConsumer>
          {({goToTodoPage}) => (
            <React.Fragment>
              <LoginForm onLogin={async (username, password) => {await login(username, password);
              goToTodoPage();
              }}/>
              localStorage.getItem('token') && <OnMount onMount={goToTodoPage}/>
            </React.Fragment>
          )}
          </PageConsumer>
        )}
      </UserConsumer>
    )
  }
}
```



##### App.js

```jsx
  import React from 'react';
  import TodoPage from './pages/TodoPage';
  import LoginPage from './pages/LoginPage';

  import {PageProvider, PageConsumer} from './contexts/PageContext';
  import {UserProvider} from './contexts/UserContext';


  export default class App extends React.Component {
    render() {
      return (
        <PageProvider>
          <UserProvider>
            <PageConsumer>
              {value => value.page === 'login' ? (
                <LoginPage />
              ) : value.page === 'todo' ? ( 
                <TodoPage />
              ) : null} 
              {/* null : 아무것도 보여주지 않는다. */}
            </PageConsumer>
          </UserProvider>  
        </PageProvider>
      )
    }
  }
```



---



### 1-3. 브라우저의 중요한 UI

- 주소표시줄, hash, 새로고침, 뒤로가기, 앞으로가기

- 사용자는 브라우저를 원래 쓰던 방식대로 쓴다.
- 사용자가 쓰던 대로 쓰더라도 잘 작동할 수 있도록 해야 한다. 

#### 1-3-1. HTML5 history API 

- https://developer.mozilla.org/ko/docs/Web/API/History_API
- DOM의 [`window`](https://developer.mozilla.org/ko/docs/Web/API/Window) 객체는 [`history`](https://developer.mozilla.org/ko/docs/Web/API/Window/history) 객체를 통해 브라우저 히스토리에 접근할 수 있다. 
- HTML5의 history 객체는 사용자 히스토리에서의 앞 뒤 이동이 가능하도록 유용한 메서드와 속성들을 제공하며, history stack의 내용을 조작할 수 있게 한다. 
  - 히스토리 : 탭마다 사용자가 이동


#### 앞으로 가기와 뒤로 가기

브라우저에서 `뒤로가기` 버튼을 누르는 것과 동일하게 작동한다

```js
window.history.back();
```



`앞으로가기` 버튼과 동일하게 작동한다

```js
window.history.forward();
```




#### 히스토리에서 특정 위치로 가기

`뒤로가기` 처럼 작동하기 위해서는 `음수`, `앞으로가기` 처럼 작동은 `양수`를 입력

```js
window.history.go(-1);
window.history.go(+1);
```



#### 히스토리 스택의 길이 측정하기 

```js
var numberOfEntries = window.history.length;
```



#### 히스토리 엔트리의 추가 및 변경

- History Stack에 내가 어떤 페이지로 접속했는지 기록이 남는다.
  - 뒤로 가기 버튼을 누를 때 마다 하나씩 제거 한다.
  - 앞으로 가기 스택이 하나 더 있다. 앞으로가기 스택에 있는 것을  History Stack에 다시 넣어준다.
  - 원래는  a 링크를 타고가야 History Stack이 추가되었다.
- HTML5는 사용자가 히스토리 엔트리를 추가하거나 변경할 수 있는 history.pushState()와 history.replaceState() 메서드를 제공한다.



##### `pushState()` 메소드 

- history stack의  항목 하나를 추가한다. 
- 주소가 바뀐다.
  - 새로고침을 하지 않고도 조작이 가능하다.

```js
var stateObj = {foo : "bar"}; 
history.pushState(stateObj, "page 2", "bar.html"); 
// 첫번째 인수 : state(상태)객체를 저장
// 두번째 인수 : title, null 넣어도 된다. (무시하기)
// 세번째 인수 : 사용자에게 보여주고 싶은 경로
```

- **state 객체** — `pushState()`에 의해 생성된 새로운 히스토리 항을 포함하고 있는 자바스크립트 객체이다. 사용자가 새로운 상태로 이동할 때 마다, `popstate` 이벤트가 발생하고, 이 이벤트의 `state` 속성은 히스토리의 `state`객체 사본을 가진다.. 

- **title** — Firefox 는 현재 이 변수를 무시한다.

- **URL** — 새로운 히스토리 엔트리의 URL을 지정한다. pushState() 호출 이후에는 브라우저가 이 URL을 로딩하지 않는 것을 명심하시기 바란다.   네트워크 통신이 일어나지 않는다.

  - 주의 !!! 

    `실행결과`는 주소창에 http://mozilla.org/bar.html를 `표시`하지만,

    - 브라우저는 bar.html `불러오지도 않으며 (실행되지 않는다)` 
    - 심지어 bar.html `파일의 존재유무를 확인하지도 않는다`.

  

##### `replaceState()` 메소드

```js
var stateObj = {foo : "bar"};
history.pushState(stateObj, "page 2", "bar.html");
```

- replaceState() 는 pustState() 와 동일하게 작동하는 것 처럼 보이지만,

  `히스토리 스택`에서 말 그대로 해당 순서의 스택에 쌓인 히스토리와 값을 `바꿔치기` 할 뿐이다



##### popstate 이벤트

- `popstate` 이벤트는 현재 활성화된 히스토리 엔트리에 변화가 있을 때 마다 실행된다.

```js
history.pushState({a:1},'','a1')
//undefined
history.pushState({a:2},'','a2')
//undefined
history.pushState({a:3},'','a3')
//undefined
window.addEventListener('popstate', e => console.log(e.state))
//undefined

// 뒤로가기 버튼 클릭
VM2068:1 {a: 2}

// 뒤로가기 버튼 클릭
VM2068:1 {a: 1}

// 앞으로가기 버튼 클릭
VM2068:1 {a: 2}

// 앞으로가기 버튼 클릭
VM2068:1 {a: 3}
```

- 리액트 라우터가 이 기술을 쓰고 있다.



#### 1-3-2. Hash Change 

```js
window.addEventListener('hashchange', e => console.log(e))
```


직접 `#` 를 이용하여 사용자가 직접 url 을 타이핑하게 되면,

```
HashChangeEvent {isTrusted: true, oldURL: "https://helloworldjavascript.net/pages/250-builtins.html", newURL: "https://helloworldjavascript.net/pages/250-builtins.html#h1", type: "hashchange", target: Window, …}
```
처럼 주소 변경된 값을 반환한다.


<br />

원하는 `#` 값을 넣은 url 을 직접 타이핑해서 조작하고 싶다면

```js
location.hash = 'bangbang'
```

`https://helloworldjavascript.net/pages/250-builtins.html#bangbang`


를 입력하면 브라우저 url 값이 변경되고 기존에 걸어둔 `이벤트 리스너`에 의해 출력된다.

```
HashChangeEvent {isTrusted: true, oldURL: "https://helloworldjavascript.net/pages/250-builtins.html#h1", newURL: "https://helloworldjavascript.net/pages/250-builtins.html#bangbang", type: "hashchange", target: Window, …}
```



---



### 1-4. React Router 

- path와 일치하면 컴포넌트를 렌더링해준다.
- exact 
  - path의 정확한 의미는 '이 문자열로 시작될 때 컴포넌트를 렌더링해줘라'
  - exact라는 분리형 프롭을 붙여주면 정확히 path에 입력한 문자열일 때만 폼이 렌더링된다. 
- 주소가 바뀌었다는 사실을 어떻게 알고 화면을 바꾸는 것일까? 
  - Router는 Provider와 유사하다.
  - Link 컴포넌트를 클릭하면 push state가 되고 라우터의 상태가 바뀐다.
  - 상태가 바뀌었으므로 다시 렌더링된다.
  - 전부 다시 렌더링되기 때문에 Route도 다시 렌더링된다. 
  - Route 컴포넌트 안에 Consumer와 유사한 놈이 있어서 제공하는 현재 주소를 받아온다.
  - 현재 주소와 일치한다면 렌더링해주고, 아니면 안해준다. 
- 주소표시줄을 바꾸는 방법
  - Link (click)
  - Redirect 

**react Router를 쓸 때는 서버 설정에 주의해야 한다.**



####  새 프로젝트 생성

```
$ npx create-react-app fds-router-practice
```

####  React router DOM 설치하기

```
$ npm install react-router-dom
```

JS 파일에서 `import` 한다

```js
import {BrowserRouter, Route, Link, Redirect} from 'react-router-dom'
```



#### 1-4-1. Basic

```jsx
import React from "react";
import { BrowserRouter as Router,   Route,   Link } from "react-router-dom";
// react-router-dom 라는 라이브러리에서 Router, Route, Link 라는 컴포넌트를 불러온다.

const BasicExample = () => ( // 함수형 컴포넌트
  <Router> {/* 라우터라는 컴포넌트로 둘러싼다. (BrowserRouter) */} 
    <div>
      <ul>
        <li>
          <Link to="/">Home</Link> 
            {/* Link 컴포넌트 :리액트라우터에서 a태그 역할을 한다. 새로고침을 안하기 위해 쓴다. */}
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
        <li>
          <Link to="/topics">Topics</Link>
        </li>
      </ul>

      <hr />

      <Route exact path="/" component={Home} /> 
        {/* 라우트라는 컴포넌트는 path, component라는 props를 받을 수 있다. 
        만약 주소창의 경로가 path의 값과 일치하면 compoent의 값을 렌더링한다. 
        exact 라는 boolean prop을 붙여주면 정확히 '/'일때만 
        exact를 붙이지 않으면 / 로 시작할 때를 말한다. */}
      <Route path="/about" component={About} />
      <Route path="/topics" component={Topics} />
    </div>
  </Router>
);

const Home = () => (
  <div>
    <h2>Home</h2>
  </div>
);

const About = () => (
  <div>
    <h2>About</h2>
  </div>
);

// Topics은 안에 중첩된 페이지가 있다.
const Topics = ({ match }) => ( // 함수형 컴포넌트 
    // match라는 props이 들어온다. path라는 prop과 현재 주소창이 어떻게 일치했는가에 대한 정보가 있다. match는 객체.
    // match.url : 현재 일치된 주소
  <div>
    <h2>Topics</h2>
    <ul>
      <li>
        <Link to={`${match.url}/rendering`}>Rendering with React</Link> 
          // topics/rendering
      </li>
      <li>
        <Link to={`${match.url}/components`}>Components</Link>
      </li>
      <li>
        <Link to={`${match.url}/props-v-state`}>Props v. State</Link>
      </li>
    </ul>

    <Route path={`${match.url}/:topicId`} component={Topic} />
        // topicId에 rendering이 들어가면 아래  {match.params.topicId}에 rendering이 들어간다.
    <Route
      exact
      path={match.url}
      render={() => <h3>Please select a topic.</h3>}
    />
  </div>
);

const Topic = ({ match }) => (
  <div>
    <h3>{match.params.topicId}</h3>
  </div>
);

export default BasicExample;
```





####  간단한 Redirect, Router 실습 예제 코드

```jsx
import React, { Component } from 'react';
import './App.css';
import {BrowserRouter, Link, Route, Switch} from 'react-router-dom';


class App extends Component {
  render() {
    return (
      <BrowserRouter>
        <div>
          <div>
            <Link to="/page1">Page1</Link>
            <Link to="/page2">Page2</Link>
            <Link to="/page3">Page3</Link>      
          </div>
          <Switch>
          {/* without adding 'exact', window returns 2 divs which are 'home' and 'page 1' */}
          {/* Depending on the situation, choose w. w/o 'exact' */}    
          {/*<Route exact path="/" component={Home} /> */}
          {/* switch : return the first address component which one has the exact same address with DOM url */}
          <Route path="/page1" component={Page1} />
          <Route path="/page2" component={Page2} />
          <Route path="/page3" component={Page3} />
          <Route path="/" component={Home} />
          </Switch>
        </div>
      </BrowserRouter>
    );
  }
}

const Home = () => {
  <div>Home</div>
}

const Page1 = () => {
  <div>Page1</div>
}

const Page2 = () => {
  <div>Page2</div>
}

const Page3 = () => {
  <div>Page3</div>
}


export default App;

```



#### 1-4-2. Redirect

- 특정 주소로 접속했을 때 사용자를 다른 곳으로 보내준다.
- 렌더링을 하는 것만으로도  주소가 바뀐다. (마치 OnMount처럼)



- 주소 표시줄의 주소를 바꾸는 방법은 두가지이다.

1. Link 컴포넌트 (사용자가 클릭을 해야만 한다.)

2. Redirect 컴포넌트

   

##### 실습

- page1로 접속하면 page2로 이동한다.

```jsx
import React, { Component } from 'react';
import './App.css';
import { BrowserRouter, Route, Link, Switch, Redirect } from 'react-router-dom';

class App extends Component {
  render() {
    return (
      <BrowserRouter>
        <div>
          <div>
            <Link to="/page1">Page1</Link>
            <Link to="/page2">Page2</Link>
            <Link to="/page3">Page3</Link>      
          </div>
          <Switch>
            {/*<Route exact path="/" component={Home} /> */}
            <Route path="/page1" component={Page1} />
            <Route path="/page2" component={Page2} />
            <Route path="/page3" component={Page3} />
            <Route path="/" component={Home} />
          </Switch>
        </div>
      </BrowserRouter>
    );
  }
}

const Home = () => {
  <div>Home</div>
}

const Page1 = () => {
  <div>
    Page1
    <Redirect to="/page2" />
  </div>
}

const Page2 = () => {
  <div>Page2</div>
}

const Page3 = () => {
  <div>Page3</div>
}


export default App;

```



#### Todo App 실습

```jsx
class PageProvider extends React.Component {
  state = {
    page: 'login'
  }
...
  // 앞으로는 주소표시줄이 페이지의 상태가 된다.


  goToTodoPage = () => {
    this.setState({
      page: 'todo'
    });
  }
  
  // Link컴포넌트가 대신하게 된다.
  
 
```

- App.js 에서 PageProvider 지우고 대신에 BrowseRouter를 쓴다.
- PageConsumer에 대한 내용을 지우고 Route들을 추가한다.
- PageContext.js 파일 삭제한다.
- LoginFormContainer.js에서  PageConsumer에 관련된 내용을 지운다.
- LogoutButtnContainer.js에서 PageConsumer에 관련되 내용을 지운다.

- http://localhost:3000/login , http://localhost:3000/todo

  - 위 주소로 접속하면 페이지가 나온다.



##### LoginFormContainer.js

```jsx
import React from 'react';
import {Redirect} from 'react-router-dom';
import LoginForm from '../components/LoginForm';
import {UserConsumer} from '../contexts/UserContext';

export default class LoginFormContainer extends React.Component {
  state = {
    success: false
  }
  render(){
    if(this.state.success) {
      return(
        <Redirect to="todo" />
      )
    } else {
      return (
        <UserConsumer>
          {({login}) =>(
            <LoginForm onLogin={async (username, password) => {
              await login(username, password);
              this.setState({success : true});
            }}/>
          )}
        </UserConsumer>
      ) 
    }
  }
}
```

##### LogoutButtonContainer.js

```jsx
import React from 'react';
import {Redirect} from 'react-router-dom';
import {UserConsumer} from '../contexts/UserContext';

export default class LogoutButtonContainer extends React.Component {
  state = {
    success: false
  }
  render(){
    if(this.state.success) {
      return (
        <Redirect to="/login" />
      )
    } else {
      return (
        <UserConsumer>
          {({logout}) =>(
            <button onClick={e => {
              logout();
              this.setState({success: true})
            }}>로그아웃</button>
          )}
        </UserConsumer>
      )
    }
  }
}
```

##### App.js 

- 맨 처음 주소에 접속했을 때 로그인이 되어있으면 todo , 로그인이 안되어있으면 login 페이지

```jsx
  import React from 'react';
  import {BrowserRouter, Route, Redirect} from 'react-router-dom';
  import TodoPage from './pages/TodoPage';
  import LoginPage from './pages/LoginPage';
  import {UserProvider} from './contexts/UserContext';

  export default class App extends React.Component {
    render() {
      return (
        <BrowserRouter>
          <UserProvider>
            <Route path="/login" component={LoginPage}/>
            <Route path="/todo" component={TodoPage}/>
            <Route exact path="/" component={Home}/>
          </UserProvider>
        </BrowserRouter>  
      )
    }
  }
  const Home = () => ( 
    //함수형 컴포넌트
    //const Home = (props) => ( // props생략
    // 괄호 안에는 표현식을 써야한다.
    localStorage.getItem('token') ? (
      <Redirect to="/todo" />
     ) : (
      <Redirect to="/login" />
     )
  )
  
```



##### TodoContainer.js

- 로그인하지 않은 사용자가 /todo 에 접속했을때 login페이지로 보내기

```jsx
import React, { Component } from 'react';
import {Redirect} from 'react-router-dom';
import TodoList from '../components/TodoList';
import TodoForm from '../components/TodoForm';
import {TodoConsumer} from '../contexts/TodoContext';

export default class TodoContainer extends Component {
  render() {
    if(localStorage.getItem('token')) {
      return (
        <TodoConsumer>
           {({todos, loading, createTodo, completeTodo, deleteTodo, updateTodoBody}) => (
          <div>
          <h1>할 일 목록</h1>
         
            <TodoForm onCreate={createTodo} />
            
          {loading ? (
            <div>loading...</div>
          ) : (
            <TodoList
              todos={todos}
              onTodoComplete={completeTodo}
              onTodoDelete={deleteTodo}
              onTodoBodyUpdate={updateTodoBody}
            />
          )}
          </div>
        )}
        </TodoConsumer>
      );
    } else {
      return <Redirect to="/login"/>
    }
  }
}

```



#### 서버 설정 

- React Router 를 쓸 때는 서버 설정을 조심해야 한다.
- localhost:3000/todo 라는 주소를 입력하면 서버에 요청이 가서 문제가 생길 수 있기 때문에 조심해야한다.

**Netlify**

- `public/_redirects` 파일 생성

```
/*  /index.html  200
```

- 한번 빌드과정을 마치면 수정이 안되기 때문에 다음에 환경 변수를 추가하면 다시 빌드를 해야한다. 

##### index.js

- Serivce Worker : 캐시를 남기게 한다.

```jsx
registerServiceWorker();
```



#### HashRouter

- HashRouter 는 BrowserRouter 를 대신하여 사용될 수 있는데, 서버를 조작할 수 없는 경우 (unlike Netlify) `HashRouter`를 사용할 수 있다.
- 코드에서 BrowserRouter 대신에 HashRouter로 변경한다.
- 다음과 같이 주소가 변경된다.

```
http://localhost:3000/#/login
```

- `#` 뒤의 해쉬부분은 요청이 가지 않는다.

- 서버 설정을 할 수 없는 경우에는 HashRouter를 쓴다.





---



## 2. Today I found out

- 혜민 : 지난 중간 프로젝트를 진행할 때 부터 궁금했던 점이 url 조작 이었는데, 오늘 그 부분에 대한 궁금점을 해결 할 수 있었어서 매우 만족스럽다!!
- 재연 : 사용자가 웹서비스를 이용할 때 불편한 점이 없도록 개선하는 방법들을 배워서 유익하였다.
- 보현 : 오늘 새로운 개념들이 많이 나와서 익숙하지 않았지만 계속 실습하면 잘 쓸 수 있을 것 같다.



---



## 3. References 


- airbnb 에서 제공하는 calendar react component with design

> https://airbnb.io/react-dates/

- React Router 공식 문서 (Basic component, Quick Start 부분도 확인)

> https://reacttraining.com/react-router/web/guides/quick-start  

- 브라우저 히스토리 조작하기 (번역문서)

> https://developer.mozilla.org/ko/docs/Web/API/sis



#### 브라우저 History 조작하기

참고 문서 :

> https://developer.mozilla.org/ko/docs/Web/API/sis



#### Deploy on Netlify using "pushState"

- Before deploy on Netlify, make sure to read 

> https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#netlify