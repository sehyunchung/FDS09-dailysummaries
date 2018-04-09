- - - 
<!-- *********8************날짜****************************** -->
# 032618 Monday  

## <strong> 1. Today I learned </strong>




<!-- *********************첫번째 제목********************** -->
### <span style="color:#595EFF"> [HTML/CSS] 1-1. 상속(Inherit) 과 종속(Cascade) </span>    

CSS 는 케스캐이드 방식을 따르고 있다고 한다. <br>
HTML 은 부모 속성의 값들을 자식이 물려받는(?) 방식.

상속은 쉽게 말해, '유전학'에 비유해서 부모의 피부색이 자식의 피부색을 결정지을 (유사하게 따라갈) 확률이 높다고 보는 식과 같다. 

`*{}`, `body{}` 전역 속성에 사용된 기본 폰트와 그 크기가 코드 전체적으로 반영되는 것은 <strong>상속</strong>의 영향이다. 

.CSS 의 모든 요소가 부모 속성의 값을 상속 받지는 않는다. 예외 사항에 대해 알고 싶다면 하단의 링크 참고. 
> https://www.w3.org/TR/CSS21/propidx.html 

<br></br>
텍스트 content가 작성된 .html 파일이 있다고 가정하고, 몇 가지 CSS 코드를 적용시켜보면.. 

```
*   {
    font-family: helvetica, arial, sans-serif;
}

body{
    font-size: 100%;
}
```
일 때,

전역 속성으로 사용된 * 의 속성값 'font-family'는 별도의 속성값이 direct 지정되어 overwrite 되기 전까지 content의 폰트가 적용된다.

<intalic>두 번째로 body에 적용된 font-size의 100% 는 어떤 font 의 size 의 배율일까?</intalic><br>
여기서의 배율 기준은 "Web Browser"의 기본 폰트 사이즈 (ex. 16px)을 기준으로, 할당된 배율의 크기만큼 폰트 값이 상속 및 반영된다.

따라서, CSS에서 상속을 이야기할 때는 무조건 부모의 값만 받아오는 것은 아니고, 또한 부모가 갖은 모든 상속값을 자식이 할당받는 것도 아니라는 점에 유의하여야 한다.

<br></br>
CSS 의 약자 풀이부터 본다면 종속(Cascade)가 얼마나 큰 영향력을 행사하는 지 알 수 있다.<br>
<strong>CSS: Cascading Style Sheet. </strong>
여러 가지 선언들을 하나의 요소에 적용하면서 충돌을 피하는 규칙을 말한다. 기준은 
- 중요도
- 명시도
- 소스 순서

<strong>중요도</strong>는 아래와 같은 순서로 뒷 쪽 순서일수록 더 큰 영향력을 갖는다. (Overwrite된다)
1. 인터넷 브라우저의 기본 스타일시트
2. 사용자(Personal)의 스타일시트의 일반 선언
3. 저작자(배포자)의 스타일시트의 일반 선언
4. 저작자의 스타일시트의 !important

<strong>명시도</strong>는 명시도 기준 계산에 따라 높은 값을 갖는 것이 보여진다.
1. `<style="">` 선언 값은 1 또는 0 
2. 선택자에 들어있는 ID 의 갯수
3. 선택자에 들어있는 class 와 가상(Pseudo) 클래스의 갯수
4. 선택자에 들어있는 요소와 가상 요소의 갯수

마지막으로 <strong>소스의 순서</strong>는 위의 모든 기준이 동일한 상태에서 가장 마지막에 선언된 값이 선택되어 보여지게 된다.. 

---

TIPS :부모의 속성값을 자식에게 강제 상속하고 싶은 경우 
```
color: inherit;
```
처럼 선언하게 되면 해당 요소의 부모의 color 속성값을 상속받아 온다. 


<br></br>
<!-- ***********************두번째 제목******************** -->
### <span style="color:#595EFF"> 1-2. 외부 파일 연결 </span>

Markup을 하다보면 외부에서 작성된 파일과 연동을 시켜야 하는 경우가 있다. <br>

예를 들어 
- Google 웹 font에서 원하는 폰트를 불러와 적용하고자 할 때
- 세분화된 .css / .scss 파일을 서로 링크시킬 때
- 타인의 bootstript, Javascript 파일들을 불러와 활용하고자 할 때 <br>

등 다양한 이유에서 외부 파일을 불러와 사용해야 하는 경우에 대비해 방법을 알아보자. 

1. link 태그를 이용한 방법
```
<link rel="stylesheet" href="style.css">
```
와 같이 html `<head>` 태그 안에서 선언한다. 구글 웹 폰트의 데이터를 활용하고자 하는 경우에는 href="(insert a generated url from Google)" 를 입력하면 된다.

2. @import 를 활용
```
@import url("_fonts.scss");
```
와 같이 .css 파일 최상단에 입력하여 원하는 파일을 링크시킬 수 있다.

위 태그를 활용하면 끝없이 길어지는 css marktp 코드를 간단한게 줄일 수 있으며, 이는 차후 코드의 유지보수에도 효과적이다. 




<br></br>
<!-- ***********************세번째 제목******************** -->
### <span style="color:#595EFF"> 1-3. Native VS. ARIA role model </span>

- Native:<br>
Header, Nav, Main 등의 Semantic 태그를 사용하여 보다 직관적인 코드를 짤 수 있음.

- ARIA 역할 모델:<br>
`div role=""` 선언으로 요소의 역활(role)을 부여하여 robot 의 코드 가독성을 높여줄 수 있음.


<br></br>
<!-- ***********************네번째 제목******************** -->
### <span style="color:#595EFF"> 1-4. Web Font의 이해 </span>

Safari, fireFox, IE 등의 인터넷 브라우저 마다 지원하는 기본 글꼴이 다르다. 따라서, 디자이너가 굳이 원하는 글꼴이 웹 페이지에 반영되기 위해서는 지정된 글꼴을 우선 사용하도록 선언이 필요하다. 

```
Font Family: Arial(글꼴이름A), Helvitica(글꼴이름B), San-serif(글꼴군- 예비)
```

대표적 generic font family (글꼴군)
- Serif : 획의 흘림과 삐침이 존재. Safari 기본 글꼴군
- Sans-serif : 고딕체. Google Chrome은 sans-serif 를 기본 글꼴군으로 지원




<br></br>
<!-- ***********************다섯번째 제목******************** -->
### <span style="color:#595EFF"> 1-5. Float와 Clearfix 활용 </span>

레이아웃을 잡기 위해 float를 사용한 경우, section의 height 값이 읽히지 않아 다음 section이 그 자리만큼 올라와 '겹친' 상태를 해결하기 위해 clearfix 모듈을 사용해야 한다.

float 에러(아닌 에러)를 수정하는 방법에는

1. `overflow: hidden`
    - 일명 뒷걸음치다 개구리 잡은 격의 해결법! 하지만 만능은 절대 아니다. 레이아웃의 크기가 변하는 순간 보여야 할 컨텐츠가 짤려나갈 수 있음.

2. 의미없는 빈 엘리먼트를 이용해 clear
    - section 제일 하단에 빈 엘리먼트(ex. div)를 넣고 `clear:both` 속성을 부여하여 float로 인해 사라진 height 값을 기계로 하여금 읽히게 함.

3. 가상 요소 선택자 `.::after` 를 활용
    - 가상요소 선택자 ex. ::before, ::after 로 기계가 무시해도 되는 가상의 요소를 만들고 이를 block 속성을 갖게 한 후 `clear:both` 를 선언해준다. 단순히 float 만을 위한 불필요한 div 생성 남발을 방지할 수 있다. 






<br></br>
## <strong> 2. Today I found out </strong>

- ::before ::after 등 Pseudo code의 이해 
    - 가상의 element 선택자를 활용한 css 기법 ex. to fix float error.
<br></br>
- display: none 과 visibility: hidden 의 차이 
    - display:none -> 해당 영역의 컨텐츠를 hide 시키고, 그 영역 또한 invisible.
    - visibility:hidden -> 해당 영역의 컨텐츠를 hide but, 빈 영역은 살아있다.
<br></br>
- 제너럴하게 사용되는 요소는 모듈화하여 외부 파일로 만들어 따로 관리할 수 있다.
    - ex. offScreen, clearfix etc.





<br></br>
## <strong> 3. 오늘 읽은 자료 (혹은 참고할 링크, 생략해도 됨) </strong>

To get used to flexbox through a web game 2..
- https://preview.webflow.com/preview/flexbox-game?preview=d1a26b027c4803817087a91c651e321f&m=1


to inderstand Inherit & Cascade written in Korean..
- http://www.clearboth.org/28_inheritance_and_cascade/

to understand how to use `link` and `@import`..
- http://triki.net/triki/html-load-css-link-import-1733
- - - -
