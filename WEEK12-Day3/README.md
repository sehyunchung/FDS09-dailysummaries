# Fastcampus Frontend Dev SCHOOL(2018.06.08)

[강의자료](https://github.com/ulgoon/fds-se/blob/develop/handouts/day01-git%2CSE.md)

## 들어가기 앞서

웹은 앱처럼, 앱은 웹처럼 서로 확장성을 가진 어플리케이션을 만들려고 하고 있다. (PWA)  
생태계가 매우 빠르게 변화하기에 우리는 빠르게 다양한 것을 배우고 습득할 수 있어야 한다.
공부의 생활화가 중요하다  
[www.google.com/IO/2018](https://events.google.com/io?gclid=CjwKCAjwr-PYBRB8EiwALtjbz-Xw933MJ3vt6Eua-PEK3qc1urC5CcvpbTu5H-_J2q_hYyh-6XwAwBoCU1gQAvD_BwE)

- 다양한 정보를 많이 얻을 수 있다.
- PWA 관련 세션.
- 이번 Google 화제는 Duplex(google assistant)

PWA: 웹앱의 경계를 허무는 웹 브라우저 위에서 동작하는 웹 사이트가 앱 환경에서도 동작하는...(노티 띄워보기)

웹은 빠른 속도로 발전 중...

PWA 와 인공지능 조합

[Apple 의 WWDC]

클라우드 서비스 : AWA, AZURE, Google Cloud service

[postgreSQL](https://www.postgresql.org/)

## git, Software Engineering

---

## git is..

---

- VCS, Source code management
- git 은 형상관리시스템으로 버젼과 소스코드를 관리한다.<br>
- Linus Torvalds 가 만들었다.(리눅스 만드신 분)
- remote repository: 깃헙, 깃랩, 빅버킷
  <br>

## git Process and Command

---

- workspace : 내컴퓨터
- remote repository : 깃허브 저장소
- git init 을 한 순간 index, local repository 가 생겨난다.

![git transport commands](https://i.stack.imgur.com/MgaV9.png)

`git remote add origin(별칭/origin 이라고 하는 관례가 있긴함) git@github.com:leekeunhwan/Git_Study.git(주소)`<br>
`git remote get-url origin(별칭)`/`git remote -v` 라고 하면 이게 무엇인지 확인하기 좋다.<br>
`git add .` (생성 및 변경된 파일을 모두 스테이징 영역에 추가)<br>
`git add "파일명"` (해당 파일만 스테이징 영역에 추가)<br>
`git reset` / `git rebase` (add/commit 초기화)<br>
`git clean -f` (untracked 파일을 모두 지울 수 있다)<br>
`git clean -fd` (untracked 파일과 디렉토리를 모두 지울 수 있다.)<br>
서로 연관이 없는 파일의 경우 add .로 싸잡아서 올리는 건 좋지 못하다.<br>
연관이 있는 것은 한번에 올려도 되지만 아닌 경우에는 따로따로 올려준다.<br>

---

## 막간을 이용한 Vim 명령어

`"Esc"`를 눌러야 명령어 모드로 바뀐다. 그 다음에 :(쉬트로+세미콜론키)을 누르고 명령어를 입력합니다.  
명령어 설명 // [ ](각괄호)안의 글자는 생략해도 됩니다.  
`:w`[rite] 저장 // :(콜론)을 누른 다음에 w 를 입력한 것입니다. :w # 처럼 숫자(#는 숫자입력을 표시)에 해당하는 파일 이름을 저장할 수 있다.  
`:sav`[eas] # // #(숫자를 의미)에 해당하는 파일을 '다른 이름'으로 저장한다.  
`:w` file.txt // file.txt 파일로 저장  
`:w »` file.txt // file.tx 파일에 덧붙여서 저장  
`:q` // vi 종료  
`:up` // 바뀐 내용만 저장합니다.  
`:x` // :upq 와 같은 내용입니다.  
`:q!` // vi 강제 종료
`ZZ` // 저장 후 종료  
`:wq!` // 강제 저장 후 종료  
`:e` file.txt // file.txt 파일을 불러옴  
`:e` 현재 파일을 불러옴  
`:e#` 바로 이전에 열었던 파일을 불러 옴

---

## My First Github Pages

github 저장소를 활용해 정적인 사이트 호스팅이 가능
`username`.github.io
http://tech.kakao.com/
https://spoqa.github.io/

---

### sample index page

After create new repo throuch github,  
`$ git clone https://github.com/username/username.github.io.git`  
Create New file `index.html`  
`$ git add .`  
`$ git commit -m "first page"`  
`$ git push origin master`

---

### sample index page

```html
<!doctype html>
<html>
 <head>
  <meta charset="utf-8">
  <title>My first gh page</title>
 </head>
 <body>
  <h1>Home</h1>
  <p>Hello, there!</p>
 </body>
</html>
```

---

### Static Site Generator

- [Jekyll](https://jekyllrb.com/): Ruby 기반 정적인 블로그 생성기
  - 설치와 사용이 쉬움
  - 사용자가 많았음
- [Hugo](https://gohugo.io/): Golang 기반 정적인 블로그 생성기
  - 빠른 속도로 사이트를 생성
  - 사용자 증가 중
- [Hexo](https://hexo.io/): Node.js 기반 정적인 블로그 생성기
  - Node.js 를 안다면 커스터마이즈가 쉬움
  - 빠른 속도로 사용자 증가 중
  ```sh
  npm install hexo-cli -g
  hexo init blog
  cd blog
  npm install
  hexo server
  ```
  **Recommand**  
  `Jekyll` > `Hugo` > `Hexo`

---

## What is branch?

![](https://www.sideshowtoy.com/assets/products/3005011-groot/lg/marvel-guardians-of-the-galaxy-groot-premium-format-3005011-02.jpg)
그런트의 몸통 - master branch  
그런트의 가지 - brunch

---

## What is branch?

분기점을 생성하고 독립적으로 코드를 변경할 수 있도록 도와주는 모델  
(master 는 사용자가 보게될 정식 버젼만 있어야 한다. / master 에서 일하면 혼나는 지름길..)  
ex)
master branch

```python
print('hello world!')
```

another branch

```python
for i in range(1,10):
    print('hello world for the %s times!' % i)
```

---

## Branch

분기점을 생성. 독립적으로 코드를 변경할 수 있도록 도와주는 모델

```sh
# {clone을 받은 repo에 어떤 브랜치가 존재하는지 확인}
git branch
# * master
git branch -a(all)
# * master
#   remotes/origin/masters
git branch -r(remote : github server 쪽)
#   origin/master
$ git branch stem
$ git branch
# * master
#   stem
$ git branch -r
#   origin/master
#   {push하지 않았기 때문에 stem이 반영되지 않았다.}
$ git checkout stem
#   Switched to branch 'stem'
$ git branch
#   master
# * stem     {*(현재 브랜치)의 위치가 바꼈다.}
```

---

파일 수정 후

```sh
$ git status
# On branch stem
# Changes not staged for commit: ....
# modified:   index.html....
$ git add index.html
$ git status
$ git commit -m "edit index.html
> set viewport width: device-width, inital-scale: 1.0
> let a, b == 1, 2;"
$ git branch
#   master
# * stem
$ git checkout master
# Switched to branch 'master'
# Your branch is up-to-date with 'origin/master'.
$ git branch
# * master
#   stem
$ cat index.html
# {stem에서 수정한 부분이 반영되지 않아 있다.}
# {날짜로 브랜치를 따서 학습 내용 정리 후, 붙이는 식으로 해보자}
```

---

remote 에서 stem 의 존재를 알게 해보자

```sh
$ git checkout stem
# Switched to branch 'stem'
$ git branch
#   master
# * stem
$ git branch -a
#   master
# * stem
#   remotes/origin/master
$ git branch -a
#   master
# * stem
#   remotes/origin/master
#   remotes/origin/stem
```

---

모든 기능이 정상동작하는 것을 확인했고 master 에 반영하고 싶을 때

```sh
$ git checkout master
# Switched to branch 'master'
# Your branch is up-to-date with 'origin/master'.
# {stem에서 master를 땡기면 안된다. master로 먼저 이동하자}
$ git branch
# * master
#   stem
# {master에서 stem의 내용을 merge하도록 하자}
$ git merge stem
# Updating 6f87bf1..228a70d
# Fast-forward {stem은 분기점에서 한시점 앞서있기 때문에 나타남}
#  index.html | 7 +++++++
#  1 file changed, 7 insertions(+)
# {master의 시점을 강제로 앞으로 땡기는 작업}
$ cat index.html
# {stem 브랜치에서 수정했던 내용이 master에도 반영된 것을 알 수 있다.}
```

---

conflict 발생

```sh
$ git branch 20180608
$ git branch
#   20180608
# * master
#   stem
$ git checkout 20180608
# Switched to branch '20180608'
$ vi index.html
# {내용 수정}
$ git status
$ git add index.html
$ git commit -m "edit index.html
> add feat: c = a + b;"
$ git checkout master
# {master 브랜치로 이동해서 충돌을 내보자}
$ vi index.html
# {내용 수정}
$ git add index.html
$ git commit -m "edit index.html
> remove feat: var a, b
> add feat: console.log"
# [master 291d566] edit index.html remove feat: var a, b add feat: console.log
# 1 file changed, 1 insertion(+), 4 deletions(-)
```

※ master 위에서 절대로 일하지 말자!(develop 브랜치에서 작업하자.)

---

conflict 해결

```sh
$ git merge 20180608
# Auto-merging index.html
# CONFLICT (content): Merge conflict in index.html
# Automatic merge failed; fix conflicts and then commit the result.
# {충돌이 발생했다.}
$ vi index.html
# <!doctype html>
# <html>
# <head>
#   <meta charset="utf-8">
#   <meta name="viewport" content="width=device-width, inital-scale=1.0">
#   <title>First page</title>
#   <script>
#   <<<<<<<<<<<<<<<
#   console.log()
#   ========
#   var a, b;
#   a = 1;
#   b = 2;
#   c = a + b;
#   >>>>>>>>>>>>>>>
#   </script>
# </head>
# <body>
# <h1>Home<h1>
# <p>
# Lorem ipsum dolor sit amet consectetur, adipisicing elit. Eaque veritatis dolore
# earum et ducimus perspiciatis sed voluptatum perferendis, corrupti facilis fuga optio velit # ipsum hic molestias dolorum labore debitis dolores.
# </p>
# {꺽쇠 부분에서 `=====`위아래 둘 중 하나를 선택하자(하나를 살리고 나머지는 지우자)}
$ git add index.html
$ git commit -m "solve conflict:
in index.html
select 20180608's content"
```

---

충돌을 내지 않고 master 와 branch 에서 작업

```sh
$ git branch
#   20180608
# * master
#   stem
$ git branch 20180608-2
$ git branch
#   20180608
#   20180608-2
# * master
#   stem
$ git branch 20180608-2
$ git branch
#   20180608
#   20180608-2
# * master
#   stem
$ git checkout 20180608-2
# Switched to branch '20180608-2'
$ git branch
#   20180608
# * 20180608-2
#   master
#   stem
# {브랜치로 가서 파일을 수정해보자}
$ vi index.html
$ git add index.html
$ git commit -m "edit index.html
> edit h1 tags innerHTML -> HOOOOOOOOME"
# [20180608-2 5fd8cff] edit index.html edit h1 tags innerHTML -> HOOOOOOOOME
#  1 file changed, 1 insertion(+), 5 deletions(-)
$ git checkout master
# Switched to branch 'master'
# Your branch is up-to-date with 'origin/master'.
# {master에서도 파일 내용을 수정해보자}
$ vi index.html
$ git add index.html
$ git commit -m "edit index.html
> add tag h3 this is home
> edit tag h1 innerHTML"
# [master 10cd3f1] edit index.html add tag h3 this is home edit tag h1 innerHTML
#  1 file changed, 3 insertions(+), 3 deletions(-)
# {master와 20180608-2브랜치에서 시점이 각각 하나씩 증가했다.}
# {한 repo에서 하다보니 pull이 아닌 merge 개념으로 해보는}
$ git push origin master
# Counting objects: 3, done.
#    6b83177..10cd3f1  master -> master
# {remote의 master를 먼저 변화시키고}
$ git checkout 20180608-2
# {브랜치에서 마스터의 최신 내용을 받아온다.}
$ git pull origin master
# From github.com:chiabi/empty-repo
#  * branch            master     -> FETCH_HEAD
# Auto-merging index.html
# CONFLICT (content): Merge conflict in index.html
# Automatic merge failed; fix conflicts and then commit the result.
# {충돌이 났지만 해결해보자}
$ vi index.html
# {꺽쇠에서 마스터와 브랜치의 내용을 선택해서 받아오자}
$ git add index.html
$ git commit -m "solve confilct:
> h1 from master
> h3 from 20180608-2"
# {브랜치에서 push를 한다}
$ git push origin 20180608-2
# * [new branch]      20180608-2 -> 20180608-2
# {master로 다시 넘어와서}
$ git checkout master
# Switched to branch 'master'
# Your branch is up-to-date with 'origin/master'.
$ git merge 20180608-2
# {브랜치의 내용과 merge하지만 충돌은 일어나지 않는다.}
#Updating 10cd3f1..e6ed858
#Fast-forward
# index.html | 9 ++++-----
# 1 file changed, 4 insertions(+), 5 deletions(-)
$ git push origin master
# Total 0 (delta 0), reused 0 (delta 0)
# To git@github.com:chiabi/empty-repo.git
#    10cd3f1..e6ed858  master -> master
```

※ bash on ubuntu on windows: 윈도우 스토어에서 받을 수 있다.(충돌이 덜 난다.)

---

## git flow strategy

## ![](https://cdn-images-1.medium.com/max/1400/1*9yJY7fyscWFUVRqnx0BM6A.png)

처음 repository 를 생성하면 develop branch 까지 만들고 fork

- master
- hotfix: 버그가 발견 되었을때 따서 작업하고 마스터와 develop 에 같은 작업을 넘겨준다.(심각한 결함이 발견되었을때 바로 고치기 위해 사용)
- release: 주석지우고, minify(uglify)하고, 최종적 테스트가 끝나면 master 로 올려준다.
- develop: 개발용 브랜치, 개발 완료하면 release 로 올린다.
- feature: develop 에서 따와서 작업 ( 로그인 기능, 장바구니 기능 기능단위)

```sh
$ git init
$ git flow init
# {develop으로 넘어온다}
$ git flow feature start home-init
# {feature/home-init으로 넘어온다}
# {... git add, git commit 작업들... }
$ git flow feature finish home-init
# {develop으로 넘어온다.}
```

## use git flow easily!

[Link](https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html)
![](https://danielkummer.github.io/git-flow-cheatsheet/img/git-flow-commands.png)

---

## Method 1: Collaboration

Add Collaborator
<img src="./image/collaborators.png">

---

## Collaboration

## Add, Commit and Push like you own it.

## Method 2: Fork and Merge

## <img src="./image/fork1.png">

## Fork and Merge

## <img src="./image/fork2.png">

## Fork and Merge

## <img src="./image/fork3.png">

## Fork and Merge

## `$ git clone https://github.com/username/forked-repo.git`

## Fork and Merge

`$ git branch -a`  
`$ git checkout -b new-feature`

---

## Fork and Merge

Make some change
`$ git add file`  
`$ git commit -m "commit message"`  
`$ git push origin new-feature`

---

## Fork and Merge

## <img src="./image/pr1.png">

## Fork and Merge

## <img src="./image/pr2.png">

## Fork and Merge

## <img src="./image/pr3.png">

## Fork and Merge

## <img src="./image/pr4.png">

## Fork and Merge

## <img src="./image/pr5.png">

## Fork and Merge

## <img src="./image/pr6.png">

## Fork and Merge

<img src="./image/pr7.png">

## Software Engineering

---

### Definition

Software engineering (SWE) is the application of engineering to the design, development,  
implementation, testing and maintenance of software in a systematic method.

> 소프트웨어의 개발, 운용, 유지보수 등의 생명 주기 전반을 체계적이고 서술적이며 정량적으로 다루는 학문

---

## Software Engineering

### Why??

---

## Development vs Implementation

- Development - The process of analysis, design, coding and testing software.<br/>
  (프로그램의 생명주기를 처음부터 끝까지 함께할 수 있는 사람)<br/>
- Implementation - The installation of a computer system or an information system. - The use of software on a particular computer system.

---

## Trend of Software Engineering

- Acceleration of **DevOps** adoption (DevOps 채택 가속화)
- Continued wave of everything natively mobile (계속되는 네이티브 모바일의 물결)
- Greater demand for increased privacy (개인 정보 보호에 대한 요구 증가)
- Cloud computing will be a thing of the past (클라우드 컴퓨팅은 과거의 일이 될 것입니다.)
- integration with Web and Mobile App (웹 및 모바일 앱과의 통합)

---

## DevOps

- 오퍼레이션이 할 일을 개발팀이 흡수했다고 생각하면 됨
- 기존의 개발과 운영 분리로 인해 발생하는 문제들  
  문제 발생 -> 비방 -> 욕 -> 상처 -> 원인분석 -> 문제해결
- Architect: 시스템의 전반적인 것을 설계
- User Reseacher: 사용자가 원하는 서비스를 분석, 실수요를 분석
- UX: User reseacher 의 분석 내용을 바탕으로 화면을 디자인
- 좋은 소프트웨어를 위한 필수조건
  - 기획팀과의 원활한 소통으로 요구사항을 충실히 반영
  - 운영팀과의 원활한 소통으로 소비자 불만과 의견을 반영
- 운영과 개발을 통합하여 커뮤니케이션 리소스를 줄이고, 개발 실패 확률을 줄임과 동시에 보다 안정적인 서비스를 운영할 수 있음!!

![](http://cfile5.uf.tistory.com/image/226C914F528B70D33266F5)

---

## Software Development Life Cycle

---

## Requirements Analysis

> 나에게 돈을 주는 사람에게 만족도를 주는 것만큼 중요한 것이 없다.

- 요구사항 유도(수집): 대화를 통해 요구사항을 결정하는 작업<br>
  (수집을 잘못하게되면 다 틀어지므로 제일 중요하다고 할 수 있다.)<br>
- 요구사항 분석: 수집한 요구사항을 분석하여 모순되거나 불완전한 사항을 해결하는 것
- 요구사항 기록: 요구사항의 문서화 작업

### Requirements

> 무엇이 구현되어야 하는가에 대한 명세

- 시스템이 어떻게 동작해야 하는지 혹은 시스템의 특징이나 속성에 대한 설명

### Requirements Analysis

- 시스템 공학과 소프트웨어 공학 분야에서 수혜자 또는 사용자와 같은 다양한 이해관계자의 상충할 수도 있는 요구사항을 고려하여 새로운 제품이나 변경된 제품에 부합하는 요구와 조건을 결정하는 것과 같은 업무

- 나(개발자)와 클라이언트(사장) 모두를 만족시키기 위한 연결고리

---

## Requirements Layer

## <img src="./image/r-layer.png">

## Business Requirements

> "Why"  
> "왜" 프로젝트를 수행하는지

- 고객이 제품을 개발함으로써 얻을 수 있는 이득
- Vision and Scope(비전과 범위)

---

## User Requirements

> "What"  
> 사용자가 이 제품을 통해 할 수 있는 "무엇"

- Use cases, Scenarios, User stories, Event-response tables, ..

---

### use case diagram

## ![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1d/Use_case_restaurant_model.svg/320px-Use_case_restaurant_model.svg.png)

### user scenario

## ![](http://www.parachutedigitalmarketing.com.au/wp-content/uploads/2012/08/Website-User-scenario-workflow.png)

### user stories

## ![](https://i17yj3r7slj2hgs3x244uey9z-wpengine.netdna-ssl.com/wp-content/uploads/edd/2016/03/BDUK-63-User-Story-Map-Template-Agile-v05-2-releases-850x600.png)

## Functional Requirements

> "What"

---

## Functional Requirements

> 개발자가 이 제품의 "무엇"을 개발할 것인지

- '~ 해야 한다' 로 끝나 반드시 수행해야 하거나 사용자가 할 수 있어야 하는 것들에 대해 작성

---

## System Requirements

- 여러개의 서브 시스템으로 구성되는 제품에 대한 최상위 요구사항을 설명
- 컴퓨터: 모니터 + 키보드 + 마우스 + 본체 + 스피커<br>
  (Express.js 6.0 버전을 쓰자 - 이런식으로 구체적으로 명시하는게 좋다)<br>

---

## Business Rules

- 비즈니스 스트럭쳐의 요구나 제약사항을 명세
- "유저 로그인을 위해서는 페이스북 계정이 있어야 한다."
- "유저 프로필 페이지에 접근하기 위해서는 로그인되어 있어야 한다"

---

## Quality Attribute

- 소프트웨어의 품질에 대해 명세
- "결제과정에서 100 명의 사용자가 평균 1.5 초의 지연시간 안에 요청을 처리해야 한다"
- 용량, 시간, 처리속도에 관련 된 사항 명세

---

## External Interface

- 시스템과 외부를 연결하는 인터페이스
- 다른 소프트웨어, 하드웨어, 통신 인터페이스, 프로토콜, ..

---

## Constraint

- 기술, 표준, 업무, 법, 제도 등의 제약조건 명세
- 개발자들의 선택사항에 제한을 두는 것

---

## When the well is full, it will run over.

---

## 지나치게 자세한 명세작성

- 명세서는 말 그대로 명세일 뿐, 실제 개발 단계에서 마주칠 모든 것을 담을 수 없음
- 개발을 언어로 모두 표현할 수 없음
- 명세서가 완벽하다고 해서 상품도 완벽하리란 보장은 없음
- 때로는 명세를 작성하기 보단 프로토타이핑이 더 간단할 수 있음.
  <style>
  h1,h2,h3,h4,h5,h6,
  p,li, dd {
  font-family: 'Nanum Gothic', Gothic;
  }
  span, pre {
  font-family: Hack, monospace;
  }
  </style>

## Q&A

[메일보내기] me@ulgoon.com

## 과제 - 메디컬 팩토리 - 로그인, 회원가입, 리뷰 : Reverse Engineering

1.  명세 - 이 기능을 구현하기 위해서 어떠한 명세가 나왔을까 적어보기(기능 명세)

---

# Git Reference

## 영역의 구분

**영역 구분**

- 워킹 트리 working tree (workspace)
- 인덱스 index (planned tree, staging area)
- 로컬 브랜치(현재 브랜치) local branch[local repository]
- 리모트 트래킹 브랜치 remote tracking branch[local repository] : 리모트 브랜치를 로컬에서 참조가능(fetch 명령으로 갱신)
- 리모트 브랜치 remote branch[remote repository]

---

**1. 워킹트리  → 인덱스**

`git status` : 워킹트리에서 아직 인덱스에 add 되지 않은 파일내역

`git diff` : 워킹 트리와 인덱스간 소스내용 차이점

`git diff <파일명>` : 해당 파일에 대한 워킹트리와 인덱스간 소스내용 차이점

**2. 인덱스  → 로컬브랜치**

`git status` : 인덱스에서 아직 commit 되지 않은 파일내역

`git diff --cached` : 인덱스와 로컬브랜치(HEAD) 간의 차이점. "commit"명령을 수행할 경우 반영되는 내용들

**3. 워킹트리  → 로컬브랜치**

`git diff HEAD` : 워킹 트리와 로컬 브랜치(head)의 소스내용 차이. 마지막 commit 이후 변경사항. "commit -a" 명령을 수행할 경우 반영되는 내용들

`git diff HEAD --<파일명>` : 해당 파일에 대한 워킹트리와 마지막 commit 이후의 소스내용 차이점

**4. 워킹트리 → 리모트 브랜치**

`git diff FETCH_HEAD` : 워킹트리와 리모트 브랜치(FETCH_HEAD)의 소스내용 차이점

`git diff FETCH_HEAD --<파일명>` : 해당 파일에 대한 워킹 트리와 리모트 브랜치 소스내용 차이점

**5. 로컬 브랜치 → 리모트 브랜치 : Outgoing Changes**

`git log FETCH_HEAD..` : 로컬 브랜치에서 리모트 브랜치에 반영할 변경내역(커밋기록)

`git diff FETCH_HEAD..` : 로컬 브랜치에서 리모트 브랜치에 반영할 소스 변경내용

**6. 리모트 브랜치 → 로컬 브랜치 : Incoming Changes**

`git log ..FETCH_HEAD` : 리모트 브랜치에서 로컬 브랜치로 가져와야할 변경내역(커밋기록)

`git diff ...FETCH_HEAD` : 리모트 브랜치에서 로컬 브랜치로 가져와야할 소스 변경내용

**\*참고**

`git fetch` : 기본 리모트 트래킹 저장소의 브랜치들을 업데이트

`git fetch <리모트트래킹저장소> <리모트브랜치>` : 해당 리모트트래킹저장소의 리모트브랜치만 업데이트

`git remote update` : 트래킹 중인 모든 저장소들 업데이트

`git pull` : fetch 포함. 즉 FETCH_HEAD 업데이트 됨

`git log -- <파일명>` : 해당 파일의 커밋 기록 보기

`git log -p` : diff 포함해서 보기

`git log --stat` : 통계형식으로 보기

`git log -n` : 최근 n 개의 기록만 보기

`git log <since>..<until>` : 두 커밋 사이의 기록만 보기(둘 중 하나 생략시 HEAD)

`git diff --ignore-space-change` : 라인 끝 공백 비교안함

`git diff --stat` : 통계형식으로 차이점 보기

`git diff -- <파일명>` : 해당 파일에 대한 차이점 보기

`git whatchanged` : git log 와 유사함

`git show <object>` : 현재 브랜치상의 주어진 커밋에 대한 기본 정보 및 소스변경 내용(diff). obj 생략시 HEAD. log 보다 좀더 상세함

`git reflog` : 로컬 저장소 내의 브랜치들이 시간에 따라 어떻게 변경되어 왔는지 보여줌

## 작업의 취소

**1. 개별파일 원복**

`git checkout -- <파일명>` : 워킹트리의 수정된 파일을 index 에 있는 것으로 원복

`git checkout HEAD -- <파일명>` : 워킹트리의 수정된 파일을 HEAD 에 있는 것으로 원복(이 경우 --는 생략가능)

`git checkout FETCH_HEAD -- <파일명>` : 워킹트리의 수정된 파일의 내용을 FETCH_HEAD 에 있는 것으로 원복? merge?(이 경우 --는 생략가능)

**2. index 추가 취소**

`git reset -- <파일명>` : 해당 파일을 index 에 추가한 것을 취소(unstage). 워킹트리의 변경내용은 보존됨. (--mixed 가 default)

`git reset HEAD <파일명>` : 위와 동일

**3. commit 취소**

`git reset HEAD^` : 최종 커밋을 취소. 워킹트리는 보존됨. (커밋은 했으나 push 하지 않은 경우 유용)

`git reset HEAD~2` : 마지막 2 개의 커밋을 취소. 워킹트리는 보존됨.

`git reset --hard HEAD~2` : 마지막 2 개의 커밋을 취소. index 및 워킹트리 모두 원복됨.

`git reset --hard ORIG_HEAD` : 머지한 것을 이미 커밋했을 때, 그 커밋을 취소. (잘못된 머지를 이미 커밋한 경우 유용)

`git revert HEAD` : HEAD 에서 변경한 내역을 취소하는 새로운 커밋 발행(undo commit). (커밋을 이미 push 해버린 경우 유용)

**4. 워킹트리 전체 원복**

`git reset --hard HEAD` : 워킹트리 전체를 마지막 커밋 상태로 되돌림. 마지막 커밋이후의 워킹트리와 index 의 수정사항 모두 사라짐. (변경을 커밋하지 않았다면 유용)

`git checkout -f` : 변경된 파일들을 HEAD 로 모두 원복(아직 커밋하지 않은 워킹트리와 index 의 수정사항 모두 사라짐. 신규추가 파일 제외)

**\*참조 : reset 옵션**

`--soft` : index 보존, 워킹트리 보존 (즉 모두 보존)

`--mixed` : index 취소, 워킹트리만 보존 (기본 옵션)

`--hard` : index 취소, 워킹트리 취소 (즉 모두 취소)

**\*untracked 파일제거**

`git clean -f <파일명>` : 해당파일 제거

`git clean -f -d` : 디렉토리까지 제거

---

공식깃레퍼런스 : [https://git-scm.com/book/ko/v2](https://git-scm.com/book/ko/v2)
