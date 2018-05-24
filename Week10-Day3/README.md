##2018/05/24(목)-3조

##FDS JSON Server
서버를 사용하기 전에 아래의 설정을 해주세요.

db.default.json 파일을 편집해서 데이터 구조를 설계해주세요.
auth.config.js 파일을 편집해서 접근 권한 설정을 해주세요.
db.default.json 파일을 .data/db.json 경로로 복사해주세요.
.env 파일에서 JWT_SECRET 환경변수를 설정해주세요.
Glitch가 .data/db.json 파일의 변경사항을 에디터에서 바로 보여주지 않습니다. 데이터의 변경 여부를 확인하고 싶다면 /db 혹은 다른 경로로 요청을 보내 데이터의 변경사항을 확인하세요.


##게시판의 댓글기능추가

#index.html에 추가된내용

<template id="comments">
  <div class="comments__list">
  </div>
</template>

<template id="comment-item">
  <p class="comment-item__body"></p>
</template>




#index.js에 추가된내용


const templates = {
  comments: document.querySelector('#comments').content,
  commentItem: document.querySelector('#comment-item').content,
}


//추가
if(localStorage.getItem('token')) {
const commentsFragment = document.importNode(templates.comments, true);
const commentsRes= await postAPI.get(`/posts/${postId}/comments`);
commentsRes.data.forEach(comment => {
    const itemFragment = document.importNode(templates.commentItem, true);
    itemFragment.querySelector('.comments-item__body').textContent = comment.body;
    commentsFragment.querySelector('.comments__list').appendChild(itemFragment);
    })
    const formEl = commentsFragment.querySelector('.comments__form');
    formEl.addEventListener('submit', async e => {
      e.preventDefault();
      const payload = {
        body: e.target.elements.body.value
      };
      const res = await postAPI.post(`/post/${postId}/comments`, payload);
      postContentPage(postId);
    });
    fragment.appendChild(commentsFragment);
  }
  
  render(fragment);




##loading indicator추가하기

#index.js에 추가된내용
async function indexPage() {
  rootEl.classList.add('root--loading');                  //추가
  
  rootEl.classList.remove('root--loading');               //추가
 

#index.scss에 추가된내용
.root{
  &--loading {
    &::after {
      display: block;
      position: fixed;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      content: 'Loading...';
      background-color: rgba(0, 0, 0, 0.5);
      color: white;
    }
  }
}

#낙관적업데이트vs 비관적업데이트
1)낙관접업데이트 : 사용자입력- 화면 갱신- 통신 시작(바로 UI를 바꿔주는 방식)
    ex)Trello, google
    장점: 응답속도가 빠른 것처럼 느껴진다.(사용자가 편해짐)
    단점: 통신을 실패해을 때의 처리가 복잡해진다.(개발자가 불편해짐)

2)비관적 업데이트: 사용자입력-통신시작-통신끝-화면 갱신
    
    장점: 통신 관련구현이 단순해진다. (개발자가 편해짐)
    단점: 사용자가 화면이 갱신될 떄까지 기다려야 한다. (사용자가 불편해짐)


##댓글 삭제버튼 추가하기(by 낙관적 업데이트)    


#index.html에 추가된내용
<template id="comment-item">
  <p class="comment-item__body"></p>
  <button class="comment-item__remove-btn">삭제</button>     //추가
</template>


#index.js에 추가된내용
if(localStorage.getItem('token')) {
const commentsFragment = document.importNode(templates.comments, true);
const commentsRes= await postAPI.get(`/posts/${postId}/comments`);
commentsRes.data.forEach(comment => {
    const itemFragment = document.importNode(templates.commentItem, true);
    const bodyEl = itemFragment.querySelector('.comments-item__body');
    const removeButtonEl= itemFragment.querySelector('.comment-item__remove-btn');
    bodyEl.textContent = comment.body;
    commentsFragment.querySelector('.comments__list').appendChild(itemFragment);
    removeButtonEl.addEventListener('click', async e => {
      //p태그와 button태그 삭제
        bodyEl.remove();
        removeButtonEl.remove();
      //delete 요청보내기
        const res = await postAPI.delete(`comments/${comments.id}`)
      //만약 요청이 실패 했을경우 원상 복구(생략)
    })  
  })



  ##할일 관리 프로그램

  