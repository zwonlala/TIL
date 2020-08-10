# 이미 push 한 commit 메시지 수정하기!


[https://ssoco.tistory.com/56](https://ssoco.tistory.com/56)

<br><br>

위 블로그를 보고 하라는 대로 

>git rebase HEAD~1 -i

명령어를 작성하니 이런 에러가 발생...

![스크린샷 2020-08-10 오후 10 42 07](https://user-images.githubusercontent.com/13375734/89791939-e4c8e000-db5e-11ea-9375-26274abe05c4.jpg)

<br><br>

검색해보니...


[스택오버플로 "Forgotten rebase interactive - git" 글](https://stackoverflow.com/questions/19134845/forgotten-rebase-interactive-git)

위 상황이 나와 비슷한것 같아 답변을 보니 `git rebase --abort` 을 하라고 하는 것 같은데 

하다가 하다가 삽질을 하다가 

<br>

> rm -fr ".git/rebase-merge"

를 함.    
(이전에 커밋로그 수정하려고 git rebase 시도했다가 그냥 포기했던 뭐시기 남아있었던 듯!)

<br><br>

그리고 다시 

>git rebase HEAD~1 -i

를 하니 이런 화면이 뜨고, 블로그 설명에서 스샷에서 빨간 박스 처리 한 부분을 **reword**로 수정하라고 함!   
(여기서 난 커밋 메시지를 수정하는 줄 알고 **reword**로 수정하고 커밋 메시지를 수정하고 2번째 라인과 3번째 라인 사이에 커밋 메시지 설명을 작성하여 오랫동안 삽질하였다 ㅠ🤣😭😱)

![스크린샷 2020-08-10 오후 11 49 43](https://user-images.githubusercontent.com/13375734/89796704-ea292900-db64-11ea-8b0b-7c9cde8cff23.jpg)

<br><br>

그렇게 앞의 명령어만 **pick** 에서 **reword**로 수정하고 **`:wq`** 를 치면

![스크린샷 2020-08-10 오후 11 59 11](https://user-images.githubusercontent.com/13375734/89797287-b7336500-db65-11ea-92f9-c68a01ef0e05.jpg)


이런 화면이 뜨고 여기서 원하는 대로 커밋 로그를 수정하면 된다!!!!!!

그리고 다시 **`:wq`** 를 치고 나온 다음

<br><br>

>git push --force

를 하면 수정된 커밋 메시지가 원격 저장소에 적용된다!!!

<br><br><br><br>

참고한 글

[https://ssoco.tistory.com/56](https://ssoco.tistory.com/56)

[https://stackoverflow.com/questions/19134845/forgotten-rebase-interactive-git](https://stackoverflow.com/questions/19134845/forgotten-rebase-interactive-git)


[https://junwoo45.github.io/2019-10-23-rebase/](https://junwoo45.github.io/2019-10-23-rebase/) -> 왜 rebase 인지 그림으로 설명해주신 부분이 도움됨!

<br><br><br><br>