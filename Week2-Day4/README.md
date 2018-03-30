# 4 조 180330 수업 내용 정리

## 1. Today I Learned

---

### Grid area (main layout)

Grid Layout 에서 아이템을 배치하는 방법은 3 가지가 있습니다.

```
- 라인 번호로 아이템 배치하는 벙법          ( [ex] grid-column-start: 4; )

- grid-column과 grid-row의 단축용법     ( [ex] gird-column: 2 / 4; )

- grid-area 프로퍼티를 사용하여 배치하는 방법
```

앞의 2 가지 방법은 사전에 우리가 공부했던 내용이였기에 생략하고,<br/>
grid-area 프로퍼티를 사용하여 배치하는 방법에 대해 조금 더 알아보겠습니다.<br/><br/>

<strong>grid-area 프로퍼티</strong><br/>

grid-area 프로퍼티는 grid-row-start / grid-column-start /<br/> grid-row-end / grid-column-end 를 일일히 열거하지 않고 단축해서 사용할 수 있습니다.<br/>
padding 과 margin 의 단축용법과는 정반대의 순서를 가지고 있기에 주의해야합니다.<br/>

```css
<style>
    .box {
        grid-area : 1 / 2 / 3 / 4 ;
    }
</style>
<body>
    <div class="wrapper">
        <div class="box1">Red</div>
    </div>
</body>
```

  <img src="https://image.slidesharecdn.com/css-grid-30-fluent-2015-150422105452-conversion-gate01/95/introduction-to-css-grid-layout-23-638.jpg?cb=1429718288" width="500" height="300">
<br/><br/>

### grid-area 를 name 으로 주어 배치하기

* grid-area 를 사용하는 방법으로 한가지가 더있는데, 각 grid item 의 이름을 원하는 이름으로 `grid-area` 속성에 지정하는 방법입니다.<br/>

  ````css
  .recommend-book{
    grid-area: rb;
   }

  .news{
    grid-area: news;
  }
  .board{
    grid-area: board;
  }

   .favorite-site{
    grid-area: fs;
  }

  .twitter {
    grid-area: twit;
  }```
  ````

- Grid container 에서 grid-template-areas 속성을 이용해 나열합니다.

  ```css
  .main {
    display: grid;
    grid-template-columns: repeat(12, 65px);
    grid-template-rows: auto auto;
    grid-template-areas:
      "rb    rb    rb    rb    news news news news news news news news"
      "board board board board twit twit twit twit twit fs   fs   fs";
  }
  /* column의 시작을 맞추면 가독성이 좋다 */
  ```

* IE11 에서는 지원하지 못하므로 해당 코드를 아래 supports rule 내부에 기입할 수 있습니다.

  ```css
  @supports (display: grid) {
    /* style */
  }
  ```

* <strong style="color:cyan;">Javascript 를 이용하여 grid layout 하는 꿀팁!</strong>

  버튼을 통해 grid 를 켰다 끌수 있는 장치를 만들어 사용합니다.<br/>

  ```html
  <button class="btn-grid" type="button">Grid</button>
  ```

  ```javascript
  var container = document.querySelector(".container");
  var grid = document.querySelector(".btn-grid");

  grid.addEventListener("click", function() {
    container.classList.toggle("is-act");
  });
  ```

---

## background 관련 프로퍼티 공부 추가

### background-attachment

* 배경 이미지를 어떻게 고정할지에 대한 프로퍼티입니다.<br/>
  해당 요소에 스크롤이 있을 경우, 스크롤하여 내용을 볼 때 배경 이미지가 내용과 같이 움직일지,<br/>
  또는 배경 이미지는 고정되어 있을지 결정 할 수 있습니다.<br/>
  또한, background-position 의 기준 점을 viewport 로 변경할 수 있습니다.<br/>

  ```css
  .box {
    background-attachment: local; /* 요소 안에 고정됩니다. 요소 안을 스크롤을 할 때,
                                        이미지가 내부의 내용과 같이 움직입니다. */
  }

  .vox {
    background-attachment: scroll; /* 기본 값으로 요소에 고정되어 있습니다. */
  }

  .hox {
    background-attachment: fixed; /* background-position의 좌표를 viewport(웹 페이지 화면)를 기준으로 합니다. */
  }

  .fox {
    background-attachment: inherit; /* 부모의 속성을 상속 받습니다. */
  }
  ```

  <strong style="color:lightpink;">fixed 를 이용한 parallax scrolling 참고 사이트</strong> - 다양한 레퍼런스를 보고 활용하면 좋습니다.

  > https://www.awwwards.com/30-great-websites-with-parallax-scrolling.html

  > https://codepen.io/search/pens?q=parallax+scroll&limit=all&type=type-pens

  > https://www.creativebloq.com/web-design/parallax-scrolling-1131762

---

### 시맨틱 마크업 (Semantic Markup) - 복습

시맨틱 마크업은 어떻게 예쁘게 보여줄까라는 생각을 완전히 배제하고,<br/>
순수하게 정보를 의미에 맞게 HTML 태그를 사용해서 작성하는 것입니다.<br/>
<strong>논리적인 순서로 우선순위인 기능을 먼저 마크업</strong>합니다.<br/>
(ex) header : 로고 / 텍스트 링크(로그인,회원가입) / 검색폼(검색창, 버튼)<br/>

<img src="https://d30cz2g5jd7t8z.cloudfront.net/media/cf/a3/cfa391b0c6961710afe56a82e1b26ea0/resize/885x666/full-semantic-html5-markup-ok-kalicube.png" width=500 height=400>

> 출처 : https://www.semrush.com/blog/semantic-html5-guide

<br/>

### 시맨틱 마크업의 장점

* 접근성이 좋아집니다.
* SEO(Search Engine Optimization)
* 수정이 용이해집니다.
* 코드 가독성이 좋아집니다.
* 코드와 데이터의 재사용성이 높아집니다.
  <br/><br/>

### Semantic Tag ++ (오늘 배웠던 태그들)

* `<strong>`

  * span 태그를 이용하여 꾸밀수 있지만 의미론적으로 본다면 strong 태그가 좋습니다.

* `<em>`

  * emphasized(강조, 중요한) text 를 지정합니다.<br/>
    i 태그와 동일하게 Italic 체로 표현되며, 의미론적인 중요성을 갖습니다.<br/>

* `<figure>`

  * 사진, 도표, 삽화, 오디오, 비디오, 코드 등을 담는 컨테이너 역할을 하는 태그입니다.

  ```html
  <figure>
    <img src=”images/book_rwd.jpg” alt=”반응형웹 핵심 가이드북”>
    <figcaption> 김데레사님의 반응형웹 핵심 가이드북</figcaption>
  </figure>
  ```

- `<figcaption>`

  * figure 요소에 대한 설명하는 문구를 담는 태그입니다.<br/>
    figcaption 태그는 요소에서 한 번만 사용 할 수 있으며, (가급적 아이디를 부여해주도록 합니다.)<br/>
    figure 안에는 여러 가지의 자식 요소(img, code..)를 포함할 수 있습니다.<br/>

- `<dl>`

  * definition list 의 약자로 용어를 설명하는 목록을 만듭니다.

- `<dt>`

  * definition term 의 약자로 정의되는 용어의 제목을 넣을 때 사용합니다.

- `<dd>` - definition description 의 약자로 용어를 설명하는 데 사용합니다.<br/>

  ```html
  <dl>
    <dt>올레 1코스</dt>
        <dd>코스 :  O O 초등학교 ~ O O 해변 </dd>
        <dd>거리 : 10km(2시간 30분) </dd>
        <dd>난이도 : 중 </dd>
    <dt>올레 2코스</dt>
        <dd>코스 :  O O O O 해변 ~ O O 포구 </dd>
        <dd>거리 : 15km(3시간 45분) </dd>
        <dd>난이도 : 상 </dd>
  </dl>
  ```

  <br/><br/>

## 웹 접근성 지침 요약

---

### 인식의 용이성

1.  **적절한 대체 텍스트** alt 속성

    * 크롬 확장 openwax 로 오류 사례 체크
    * 대체 컨텐츠: 이미지 안에 정보가 많을 경우 따로 p 태그 만들어서 숨김<br/><br/>

2.  멀티미디어 콘텐츠
    * 자막과 수화 동시 제공<br/><br/>
3.  색에 무관한 콘텐츠 인식
    * 캡션 or 패턴/식별 다르게 (예: 월드컵 축구팀 유니폼)<br/><br/>
4.  명확한 지시 사항 제공
5.  텍스트 콘텐츠의 명도 대비
    * 텍스트와 배경 간의 명도 대비는 4.5 대 1 이상
    * Colour contrast Analyser<br/><br/>
6.  자동 재생 금지
7.  콘텐츠 간의 구분
8.  **키보드 사용 보장**
    * 모든 기능은 키보드만으로 사용 가능해야<br/><br/>
9.  **포커스 이동**
    * 시각적으로 구분, 논리적으로 이동 가능하게<br/><br/>
10. 조작 가능 - 링크 컨트롤 크기
11. 응답 시간 조절 - 예: 약관 동의
    * 예: 약관 동의<br/><br/>
12. 정지 기능 제공 - 자동으로 변경되는 콘텐츠
13. 깜빡임과 번쩍임 사용 제한. 초당 3~50 회 주기
14. 반복 영역 건너뛰기 - 메뉴 건너뛰고 본문으로 바로가기
15. **제목 제공**
    * 적절한 페이지 제목 title
    * iframe 에 title 속성 부여<br/><br/>
16. 적절한 링크 텍스트 - 잘못된 예: <u>여기</u>를 눌러주세요
17. 기본 언어 표시 - 해당 국가 언어 표시
18. 18. 자동 실행 컨텐츠 - 예: 자동 팝업, 뉴스 광고
19. **콘텐츠의 선형 구조**
20. 표의 구성
21. **레이블 제공**
    * 접근성도 지키면서 ui 만들기
    * input 에 label 을 줘야하지만 국내에서는 title 도 가능<br/><br/>
22. 입력 오류 정정
23. **마크업 오류 방지**
    * 열고 닫기 오류, 태그 중첩 오류, 중복된 속성 - DOM Tree 인식 문제<br/><br/>
24. 웹 애플리케이션 접근성 준수 - aria 이용

<br/><br/>

# 2. Today I Found Out

```
dl태그 내부에 div태그로 감싸는 것이 최근에 가능해졌다는 사실과 dt와 dd가 1대다 대응이 가능하다는 것을 알았습니다.
또한 다양한 접근성 사례를 접하면서, 서비스를 배포하기 전에 웹 접근성 체크리스트를 필수로 확인해 봐야겠다는 생각이 들었고,사소하다고 생각되는 부분이 사용자에게 얼마나 큰 영향을 미치는 지 알게 되었습니다.
더욱 열심히 공부하겠습니다.
```

# 3. refer

> 해당되는 내용에 추가하였습니다.
