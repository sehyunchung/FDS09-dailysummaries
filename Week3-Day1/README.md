# 4/2 (월)

## 1. Today I learned

### 1-1. Form요소 
###  input 태그 속성

+ type: 태그 모양을 다양하게 변경할 수 있다. 
####  text
```
<input type="text">
```
 + 줄바꿈이 없는 single line 텍스트이다.
 + maxlength를 사용하면 최대 글자수를 정할 수 있다.

#### search
 + 웹사이트에 검색 기능을 구현할 때 사용한다.
 + autofocus면 검색list를 볼 수 있는 기능을 추가할 수 있다.  

```
<input type="search" autofocus list="search-suggestions"/>
<datalist id="search-suggestions">
	<option label="DM" value="Depeche Mode">
</datalist>
```

#### tel
```
<input type="tel">
```
 + 사용자로부터 입력되는 데이터가 전화번호일 때 사용한다.
 + pattern=“[0-9]{10}” 이면 제한 값 0~9까지만 들어 올 수 있다.
 + 모바일 브라우저에서 키보드 배열이 변경된다. 

####  password
```
<input type="password">
```
 + text 속성과 같지만 문자를 숨겨서 표시한다. 

#### url
```
<input type="url">
```
 + 사용자로부터 입력되는 데이터가 url일 때 사용한다. 

#### email
```
<input type="email">
```
 + 사용자로부터 입력되는 데이터가 이메일 주소일 때 사용한다.
 + 이메일 형식에 맞지 않은 값을 입력하면 경고 메시지를 출력해준다. 

#### datetime
```
<input type="datetime">
```
 + 날짜나 시간을 나타낸다. 

####  날짜와 시간관련 type
 + 날짜와 시간을 선택할 수 있는 창을 만든다.
 + 키보드와 마우스 모두 접근 가능하다.
   + date
     + YYYY-MM-DD형태의 날짜를 나타낸다. 2018-04-02
   + month
     + 월을 나타낸다.
   + week
     + 주를 나타낸다.
   + time
     + 00:00 ~ 24:00와 같이 하루의 시간을 나타낸다.
   
#### date-type

```
<input type="date">
```

1. date타입은 사용자가 날짜를 입력 할 수 있도록 입력 필드를 작성한다. 자동으로 내용의 유효성을 검사하는 텍스트 상자를 사용하거나 특수한 날짜 선택기 인터페이스를 사용한다.
2. 브라우저마다 UI가 다르기 때문에  https://caniuse.com/#search=DATE 호환가능한 브라우저를 검색 하는 것이 좋다.

#### month-type

```
<input type="month">
```

1. 사용자가 월 및 연도를 입력 할 수 있도록 입력 필드를 작성하여 월 및 연도를 쉽게 입력 할 수 있도록 한다. `"YYYY-MM"`, 여기서는 `YYYY`4 자리 연도이며 `MM`, 월 이다.
2. 브라우저마다 UI가 다르기 때문에  https://caniuse.com/#search=month 호환가능한 브라우저를 검색 하는 것이 좋다.

#### week-type

```
<input type="week">
```

1. 입력 요소를 작성하여 해당 연도의 일주일에 1 년을 더한 항목 (예 : 1 ~ 52 주)을 쉽게 입력 할 수 있다.
2. 지원은 현재 Chrome / Opera와 Microsoft Edge 만 지원하므로 약간 제한되어 있다.

#### time-type

```
<input type="time">
```

1. 사용자가 시간 (시간과 분 및 선택적으로 초)을 쉽게 입력 할 수 있도록 설계 되어 있다.
2. 유일하게 사파리에서만 지원하지 않는다.

#### DateTime-Local-type

```
<input type="datetime-local">
```

1.  년, 월, 일 및시와 분을 포함하여 날짜와 시간을 쉽게 입력 할 수 있다.
2. 브라우저마다 UI가 다르기 때문에 https://caniuse.com/#search=datetime-local 호환가능한 브라우저를 검색 하는 것이 좋다.

#### number-type

```
<input type="number">
```

1. 사용자가 숫자를 입력하는 데 사용됩니다. 여기에는 문자는 입력되지 않는다.
2. min, max 최소 , 최대값을 정할 수 있다.

####  range-type

```
<input type="range">
```

1. 일반적으로 숫자 입력 유형 과 같은 텍스트 입력 상자가 아닌 슬라이더 또는 다이얼 컨트롤을 사용하여 표시 된다 . 
2. 사용자의 브라우저가 유형을 지원하지 않으면 `"range"`폴백하여 `"text"`입력 으로 처리 한다. 

####  color-type

```
<input type="color">
```

1. 시각적 색상 선택기 인터페이스를 사용하거나 색상을 `"#rrggbb"`16 진수 형식 의 텍스트 필드에 입력하여 사용자가 색상을 지정할 수 있도록하는 사용자 인터페이스 요소를 제공 한다.

####  Checkbox-type

```
<input type="checkbox">
```

1.  선택 (체크)되는 사각형 상자로 렌더링 된다.

####  Radio-type

```
<input type="radio">
```

1. 일반적으로 **라디오 그룹에** 사용되며 , 관련 옵션 세트를 설명하는 라디오 버튼 모음 이다. 주어진 그룹에서 하나의 라디오 버튼 만 선택할 수 있다. 

####  select 드롭다운

```
<select name="job">
    <option value="">직업선택</option>
    <option value="학생">학생</option>
    <option value="회사원">회사원</option>
    <option value="기타">기타</option>
</select>
```

1. select 태그는 option 태그로 구성 된다.
2. select 태그를 사용하면 드롭다운 형식으로 클릭했을때 밑으로 option 값이 나온다.

#### file-type

```
<input type="file">
```

1. 파일을 업로드 할 수 있는 입력 필드가 만들어 진다.

### 1-2. Video 
- `video` 태그는 HTML5 에서는 다른 추가 플러그인 없이 비디오와 오디오의 미디어에 대한 재생이 가능하도록 지원해준다. 동영상 콘텐츠를 포함하기 위해 사용하며 `src`속성이나 `<source>`요소를 이용해 여러개의 동영상 소스를 표시 할 수 있고 브라우저에 가장 적절한 것을 선택해서 사용한다.

  - `video` 사용 예
    ```html
    <video class="news-video" src="/media/stories.mp4" poster="/media/poster.jpg" controls preload="auto" autoplay>
    ```

- Attributes

    `src` : 삽입할 동영상의 주소, 재생할 미디어의 URL을 나타낸다  
    `height` : 비디오 높이의 픽셀 값
    `width` : 비디오 넓이의 픽셀 값  
    `controls` : 비디오의 재생, 볼륨 등 제어 조절 장치를 보여주며,  "controls"나 공백이나 태그 안에 값 없이 controls만 적어줘도 적용된다.  
    `muted` : 음소거, 비디오의 포함된 오디오를 음소거 할지 지정(기본값 false)  
    `poster` : 비디오가 로드되지 않고 있을때 처음에 표시될 이미지의 URL  
    `loop` : 이 속성이 설정 되어 있으면 동영상을 계속 반복한다.  
    `preload` : 페이지를 읽을 때 미디어도 같이 읽어들여 재생을 준비한다.

      none : 비디오 파일을 로드하지 않음
      metadata : metadata만 로드 함
      auto: 전체 비디오 파일을 로드함
         
- `track` 태그  
  트랙 엘리먼트는 미디어 요소(`audio`,`video`)의 자식 요소이며, 외국어에 대한 자막, 장애인들을 위한 자막, 스크린 리더가 읽는 글을 비디오나, 오디오에 추가를 해줄수 있도록 한다. vtt의 파일 확장자 명을 가진다.
  
  - `track` 사용 예
    ```html
    <video src="media/stories.mp4">
    <track src="media/stories_ko.vtt" kind="captions" srclang="ko" label="korean Caption"">
    <track src="media/stories_en.vtt" kind="captions" srclang="en" label="English Caption"">
    </video>
    ```
  - Attributes

      `kind`- 텍스트 트랙의 종류를 정의한다.  
      `src` - 텍스트 트랙의 데이터의 주소(.vtt 파일)를 정의한다.   이 속성은 반드시 정의가 되어야한다.  
      `srclang` - 텍스트 트랙의 데이터의 언어를 정의한다.  
      `label` - 브라우저가 사용 가능한 텍스트 트랙을 나열할 때 사용자가 읽을 수 있는 트랙제목.  
      `default` - 기본 트랙을 정의.

###1-3. CSS Image Sprites 기법

- 아이콘은 img태그를 사용해도 되지만  대체텍스트가 없는 이미지이기  때문에 background 속성을 사용하여 배경에 이미지를 깔아주는 것을 권장한다. 

- CSS sprites 기법을 사용하면 여러 개의 이미지파일을 모두 부르는것이 아니라 한 이미지파일로 통합하여 부르게 된다.  따라서 서버와의 요청 횟수가 줄어들어 로딩속도가 줄어들고 내려받는 이미지의 용량이 줄어들어 효율적이다.

- 적용하는 방법은 아이콘들이 합쳐진 큰 이미지를 background-image로 배경을 설정하고, background-position 속성을 사용하여 좌표값을 조절하여 필요한 부분만 보이도록 한다.



#### HTML

```
 <h2 class="recommend-book-heading main-section-heading">추천 서적<span class="en-heading">Recommend Book</span></h2>

 <h2 class="news-heading main-section-heading">새소식<span class="en-heading">WebCafe News</span></h2>

```

#### CSS
```
/* 메인 콘텐츠 섹션 제목 공통 */
.main-section-heading{
  background-image: url("images/sprite_main.png");
  background-repeat: no-repeat;
}

/* 추천 서적 제목 */
.recommend-book-heading{
  background-position:0 0;
}

/* 새소식 제목 */
.news-heading {
  background-position: 0 -230px;
}
```

#### background-position 
: 위쪽으로 230px 만큼 이동한다.
![background-position](./img/sprite_img.jpg)



###1-4. Icon Font
- 딩벳폰트는 폰트 대신 어떤 문자에 해당하는 이미지로 이루어진 폰트이다.
- **fontello**는 딩벳이나 아이콘을 폰트로 제공하는 여러 서비스를 모아둔 서비스이다.
#### fontello 사용법
1. [fontello](http://fontello.com/)에 들어가서 원하는 아이콘을 선택한다.
1. 선택을 마친후 오른쪽 상단에서 download 받는다.
1. 압축을 풀면 font 폴더와 css 폴더가 있는데 font 폴더를 복사하여 원하는 위치에 넣고 css폴더의 fontello.css의 코드를 원하는 위치에 넣는다.
1. 아이콘을 첨부하고 싶은 html 코드에 원하는 아이콘의 클래스명을 지정한다.
```
<ul class="fontello-list">
    <li class="icon-heart">아이콘폰트1</li>
    <li><i class="icon-glass"></i>아이콘폰트2</li>
    <li>아이콘폰트3<i class="icon-star"></i></li>
</ul>
```

[font awesome](https://fontawesome.com)도 아이콘 폰트가 가능하다.
    - acceesibility : aria-label labeledby 도 가능 / aria-hidden을 사용하면 스크린 리더가 읽지 않음


## 2. Today I found out

- 접근성을 고려하여 마크업하는것이 어려웠다. 문서를 검색해서 속성을 찾아보고 복습해봐야겠다.
- 사용자가 어떤 브라우저를 사용하는지 알 수 없는 상황에서, 어떤 브라우저든 지원하기위해 source tag를 여러 개 써서 링크하는것도 video태그를 잘 이용 하는 방법중에 하나인 것 같다.
- 아이콘을 나타내는 여러 방법을 알게 되었고 좀 더 편한 image sprites  기법도 사용해보고싶다.

## 3. 오늘 참고한 링크

[input mdn문서](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input) 

[HTML5 video 요소의 사용 예](http://craftymind.com/factory/html5video/CanvasVideo.html)

[track 요소 참고 사이트](http://html5ref.clearboth.org/html5:)

