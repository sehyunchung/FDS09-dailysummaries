# 2조 수업내용 정리
## 1.Today learnning
### inline 값의 레이아웃 간 공백의 문제
- li: 공백을 남김. `<li>`와 `</li>`사이의 줄바꿈이 숨겨져 있기 때문이다. 이것이 자식 노드가 되어서 공백을 발생시킨다.<br/>
```
    <ul class="member">
        <li> <!-- 여기 바로 이 부분!! -->
            <a href="#">로그인</a> 
        </li>
        <li>
            <a href="#">회원가입</a>
        </li>
        <li>
            <a href="#">커뮤니티</a>
        </li>
    </ul>
```
- 보완: css에서 .member의 폰트크기를 0으로 하고 개별로 li의 폰트 크기를 지정한다. (ex: 1rem) 

- 여기서, inline은 내부 콘텐츠 길이에 따라 길이가 알아서 조절되지만 상하 높이는 적용되지 않는다.
- 보완: inline-block을 사용하자.
--- 
### 44px / 7mm rule
- UI를 제작할 때, 하나의 컨트롤과 버튼은 가로 세로 각각 44px 혹은 7mm를 기준으로 하라. 이는 성인 남성의 검지 끝 면적을 기준으로 한다. 
- 그러나 44px는 쉽지 않다. 그럴 경우 최소 27px은 유지하도록 하자.
- 컨트롤, 버튼 사이에 최소 1px의 간격이 필요하다. 
### fieldset and flex
...그냥 form 상위로 div wrapper를 설정하면 안되나? semantic에서 문제가 생기나? 나중에 확인해 보도록 한다.
### Attribute Selector 
속성 선택자 : html 요소의 속성을 조회하는 선택자
`  E[name^=value] ` <br/>
> [name] 속성값이 value로 시작하는 요소
```
a[title]{

property:value;

}

: title 속성이 지정된 <a>요소를 선택
```

---
### button
버튼 클래스는 chrome, firefox 등 브라우저마다 border와 padding 등 넓이와 높이가 달라진다.
현업에서는 button클래스를 잘쓰지않는다.
a태그를 역활모델을 바꾼다.

### property position
#### absolute
- display --> block (similar with `<float>`)
- layerified
- position standartd: closest upper tag which is `position !: static` --> closeset layer
- `width: auto` trick:  ex) center positioning
#### relative
- display --> block (similar with `<float>`)
- layerified
#### decender
blank space beneath of text(inline) <br/>
- solution
- - display: value = block
- - line-height: value = 1
#### polifill
caniuse.com --> 'search' --> resources --> polyfill

---

### grid polyfill issue
#### ms prefix
`-ms-` 로 시작
#### prefix
벤더프리픽스를 표준 선언보다 앞에 위치 한다. cascading
#### Feature Queries
`@support`
> css 속성 선언에 대해서 지원하는 브라우저만 골라서 렌더링함.

---

## 2. Today I found out
### first-child
`first-child`: `::first-child` (x) `:first-child` (o). 
<!-- pseudo랑은 다른가 보네. 하긴 pseudo도 이전 버전은 `:`이라니까... -->
### grid-template
grid-template 으로 쓰기보다 grid-template-areas, gird-template-rows, grid-template-colmuns로 나누어서 사용하는 것을 하기로 하자. 이게 더 정확하다. 손이 좀 더가긴 한다만 그래도 불확실한 것 보다는 낫다.
### axis of evil
Micorsoft Internet explorer
## 3. 오늘 읽은 자료 (혹은 참고할 링크, 생략해도 됨)
### em, rem
https://webdesign.tutsplus.com/ko/tutorials/comprehensive-guide-when-to-use-em-vs-rem--cms-23984

---
**ul (unordered list)**
순서가 의미 없는 리스트를 나타냄.
ul의 자식요소로 반드시 li 요소만 포함해야 함. (다른 요소들은 자식요소가 될 수 없다.)
**li (list-item)**
ul(순서 없는 리스트), ol(정렬된 리스트)의 자식요소로 목록의 항목을 나타냄
```
<ul>
    <li>first item</li>
    <li>second item</li>
    <li>third item</li>
</ul>
```
###css 속성 적용 우선 순위
```
1. 속성 값 뒤에 !important 를 붙인 속성
2. HTML에서 style을 직접 지정한 속성
3. #id 로 지정한 속성
4. .클래스, :추상클래스 로 지정한 속성
5. 태그이름 으로 지정한 속성
6. 상위 객체에 의해 상속된 속성
```

---
### display 
*display 속성은 요소를 어떻게 보여줄지를 결정한다.*
inline : 인라인 박스
inline-block : block과 inline의 중간 형태
### inline 
요소를 inline 요소처럼 표시한다. 
html 인라인 요소로는 `<span>, <a>` 태그 등이 이에 해당됨
block 과 달리 줄 바꿈이 되지 않고, width와 height를 지정 할 수 없다.
따라서 콘텐츠의 길이 만큼 요소가 늘어나게 된다.inline-block
block과 inline의 중간 형태라고 볼 수 있는데, 줄 바꿈이 되지 않지만 크기를 지정 할 수 있다.
요소는 inline이지만 내부는 block처럼 표현된다. inline처럼 옆으로 늘어선다.
IE8부터 지원하는 속성이다. 
inline-block은 vertical-align 의 속성을 지정할 수 있다.

---
### position
relative
relative는 별도의 프로퍼티를 지정하지 않는 이상 static과 동일하게 동작하고 원래 있던 위치를 기준으로 좌표(top,right,bottom,left)를 지정할 수 있다. 좌표값으로 지정된 위치에 자식요소를 포함하여 위치가 이동하게 됨.
fixed
고정(fixed) 엘리먼트는 뷰포트(viewport)에 상대적으로 위치가 지정되는데, 이는 페이지가 스크롤되더라도 늘 같은 곳에 위치한다. relative와 마찬가지로 top이나 right, bottom, left 프로퍼티가 사용된다.
absolute
absolute는가장 가까운 곳에 위치한 조상 엘리먼트에 상대적으로 위치가 지정된다. 절대값으로 지정된 엘리먼트가 기준으로 삼는 조상 엘리먼트가 없으면 문서 본문(document body)을 기준으로 삼고, 페이지 스크롤에 따라 움직입니다. "위치가 지정된" 엘리먼트는 position이 static으로 지정되지 않은 엘리먼트를 가리킨다.

---
### 속성 선택자
아이디말고 type 속성을 css로 불러올수있다.
```
html
<input aria-label="검색어" type="search" id="search" required placeholder="검색어를 입력하세요.">
```
```
css  // 속성 선택을 할수있다.
input[type="search"]{
}
```
