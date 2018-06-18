# 6/18 (월)

## 1. Today I learend

### **children prop**
- `this.props.children`은 특별한 prop으로 태그 자체가 아닌 JSX 표현식의 자식 태그들을 정의한다.

  ```js
  import React from 'react';

  export default class Box extends React.Component {
    render() {
      return (
        <div className="box">
          {this.props.children}
        </div>
      )
    }
  }
  ```

  - 아래와 같이 사용한다면 `this.props.children`이 `<div>React</div>`을 받는다.

  ```JSX
  <Box>
    <div>React</div>
  </Box>
  ```

  - 아래와 같다고 생각하면 된다.

  ```jsx
  <Box children={<div>React</div>} />
  ```

  ```js
  import React from 'react';

  export default class Box extends React.Component {
    render() {
      const value = {
        a: 1,
        b: 2
      }
      return (
        <div className="box">
          {this.props.children(value)}
        </div>
      )
    }
  }
  ```

  ```JSX
  <Box>
    {value => <div>
      <div>{value.a}</div>
      <div>{value.b}</div>
    </div>}
  </Box>
  ```

  - 레이아웃 이라는 공통되는 컴포넌트들을 이런식으로 만들 수 있다. (sub, navebar, sidebar....)

### **비동기 시 예외처리**
- 네트워크 요청이 일어난 부분들은 `try ~ catch` 구문으로 감싸주는게 좋다.

- Axios의 error 처리 방법
  ```js
  axios.get('/user/12345')
    .catch(function (error) {
      if (error.response) {
        // The request was made and the server responded with a status code
        // that falls out of the range of 2xx
        console.log(error.response.data);
        console.log(error.response.status);
        console.log(error.response.headers);
      } else if (error.request) {
        // The request was made but no response was received
        // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
        // http.ClientRequest in node.js
        console.log(error.request);
      } else {
        // Something happened in setting up the request that triggered an Error
        console.log('Error', error.message);
      }
      console.log(error.config);
    });
  ```

- axios 는 200 번 떄가 아니면 에러를 발생시킴
  - pending 기다림
  - fulling 채워짐
  - rejected 값을 채우는 것을 실패
- 400 이면 제대로된 아이디 비밀번호가 아님
- 500 은 서버에러임   

- catch의 e라는 매개변수에 에러 객체가 들어온다.  
- axios를 사용할 경우 axios가 정의한 에러객체가 들어온다.  
  - 이러한 성질을 이용해 경우에 따른 에러 처리를 해주자  

### **제어되지 않는 컴포넌트**
- 제어되지 않는 컴포넌트는 진리의 원천을 DOM 에 두기 때문에, React 를 사용한 코드와 사용하지 않은 코드를 통합하는 작업을 좀 더 쉽게 만들어줄 수 있다.
그리고 코드의 양이 상대적으로 적다. 좀 지저분하지만 빠른 해결책을 원한다면 제어되지 않는 컴포넌트를 사용. 그렇지 않다면, 제어되는 컴포넌트를 사용

- 폼을 구현할 때에는 웬만하면 제어되는 컴포넌트를 사용하길 권함  
('항상 소문자/대문자만 입력 가능하게 한다거나 10글자만 받는다'같은 제어가 필요한 경우)  

- 제어되지 않는 컴포넌트는 상태 업데이트를 위해 이벤트 핸들러를 작성할 필요가 없다.  
대신 `ref`를 사용해 폼 데이터를 DOM으로부터 가져올 수 있다.  
(※ 주의 - 공식 문서의 예제의 ref 사용법은 옛날 방식임)

- value prop이나 onChange prop을 넣지 않고도 폼을 사용할 수 있다.

- 제어되는 컴포넌트의 존재 이유는 폼은 자체적인 상태를 가지고 있으므로 상태가 분산되어 있는 것은 좋지 않다고 생각하여 **상태를 다 리액트에서 관리하고 싶기 때문**이다.  

- 제어되지 않는 컴포넌트 특징
  + 장점: 코드의 양이 상대적으로 적다.
  + 단점: 제어되지 않는 컴포넌트는 진리의 원천(Source of Truth)을 DOM에 두기 때문에 상태 관리가 어렵다. 

### **Presentational component & Container component**
- **Presentational component** : 화면표시만을 위한 컴포넌트 
  - 외부세계와 직접 연동 되진 않지만 `prop`을 통해 간접적으로 연동될 수도 있다.
  - 어떻게 연동되는지에 따라 다목적으로 사용이 가능.
  - 중립적인 인터페이스이어야 한다. (**재사용성이 높아지기 떄문**)
  - 외부세계와 연동되지않게 설계하는것이 좋음.
- **Container component** : 외부세계와 연동되는 컴포넌트 

- `stories` : Presentational component의 테스트를 도와주는 도구

- Presentational 컴포넌트는 외부 세계와 직접적으로 연동되지 않는다. `prop`을 통해 `onLogin()`같은 것을 받아 간접적으로는 외부세계와 연동될 수 있다. 

- `Provider` 역시 컴포넌트이다. `userProvider` 같은 것이 Container 컴포넌트이다.  
Presentational 컴포넌트는 어떻게 연동하는지에 따라 다목적으로 사용할 수 있다.

  ```jsx
  // 이렇게 사용해도
  <LoginForm onLogin={onLogin}>
  ```
  ```jsx
  // 이렇게 사용해도 상관없다.
  <LoginForm onLogin={(username, password) => {
    console.log(username, password)
  }}>
  ```
- 'LoginForm을 사용하는 방법은 onLogin에 username과 password를 받는 함수를 넘겨주는 것이다.' 라는 식의 사용법을 정하여 이 사용법을 지킨다면 어떤식으로 사용하든 문제가 없도록 정의하는 것을 **인터페이스**라 한다.

- 인터페이스: 어떤 코드 집합의 사용법

- Presentational 컴포넌트는 외부세계와 어떻게 연동될지에 대한 가정을 하지 않는게 좋다. (**중립적인 인터페이스**라 한다.)   
특정 외부세계를 가정하지 않는다.  
만약 인터페이스를 중립적으로 만들었다면, 예를 들어 데모페이지와 서버와 연동되는 동일한 페이지(메모리버전 할 일 서비스, JSON서버 할 일 서비스)를 나누기 쉬울 것이다.

  + 중립적인 컴포넌트는 재사용성이 높아진다. 
  + 분업이 가능해진다. (Presentational 컴포넌트 / Context, Container 컴포넌트)

※ 약속: components 디렉토리의 컴포넌트 파일은 전부 Presentational 컴포넌트로 만든다.

## 2. Today I Found Out

- 오늘 수업도 설계에 관련된 것이라 그런지 이해가 될 듯 말듯 하다.(어렵다)
프레젠테이셔널 컴포넌트와 컨테이너 컴포넌트를 따로 분리해서 재사용성을 높이는 연습을 많이 해보고 공부해야겠다. 스토리북이라는 새로운 도구를 배웠는데, 효율적으로 잘 사용할 수 있도록 미니 프로젝트 같은 것을 할 때 적용해봐야겠다.  

- CC와 PC를 나눠주어야 하는 이유는 어느 정도 알 것 같지만 아직은 적재적소에 어떻게 구분해줘야 할지 조금은 헷갈리는 것 같다. 역시 많이 직접 쳐보면서 공부하는 방법이 본인에게 제일 적합한 방법이라 생각된다.