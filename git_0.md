## Pull Requests

> Pull requests let you tell others about changes you've pushed to a brach in a repository on Github.
>
> 풀리퀘는 당신이 변경한 내용에 대해서 다른 사람들에게 말해준다.

* commit한 내용을 master에 Merge하는 것에 대해 동의를 구하는 것

* 주요 항목
   1) 작업 제목
   2) 작업 내용
   3) Commit logs
   4) Reviewer

* 규칙
  * 1개의 PR에는 1개의 기능에 대한 변경 및 추가를 포함하는게 좋다.
  * 제목만 보고도 어떤 작업을 했는지 알 수 있도록 한 줄로 요약해서 작성.
    
    > 이슈와 관련된 PR을 작성할 때:  [Issue Number] [Behavior] Title ([참고](https://github.com/Mash-Up-MapC/MapC-backend/pull/54))
* 내용은 제목에서 적지 못한 구체적인 작업 내용 / 상황 / 관련 자료 등을 넣어서 이해를 돕는다.
  
* Pull Request 하기
```
1) 작업할 브랜치로 Checkout (git checkout <branch>)
2) 작업 내용 Commit
3) 원격 서버에 Push
4) Pull reqeusts 작성
5) 제목, 내용, 리뷰어 지정
```

* Pull Request 리뷰 하기
```
1) PR이 어떤 작업에 대한 PR인지 파악
2) 상단의 커밋 탭에서 커밋 히스토리를 살펴본다.
3) 실제로 변경된 파일들을 보면서 리뷰한다. (코멘트 달기, 재수정 요청하기 등)
   - 예시 Code 작성, 관련 기술문서, 구체적인 사례를 인용하여 코멘트를 단다.
   - 핵심만 간단히 남기고 감정을 싣지 않는다.
4) PR에 대한 전체적인 코멘트를 남긴다.
5) PR을 승인할지 재변경을 요청할지 결정한다.
   - 승인: Approve
   - 변경 요청: Request changes
```

* 병합하기
  * Create a merge commit
    - PR의 commit들이 관련 메시지와 함께 master의 Head commit으로 들어간다.
    - 메세지는 수정할 수 있으나 master에 병합될 때 log들이 지저분하게 삽입된다.
      (git merge 명령이랑 똑같다.)

  * Rebase and merge
    - PR의 log들이 master에 재정렬돼서 병합된다. 
    - 로컬에서 작성된 모든 커밋로그들까지 추적할 수 있으므로 PR의 모든 커밋들이 master에서 관리돼야한다면 이 방법으로 하는 것이 좋다.

  * Squash and merge
    - PR의 log들을 한개로 정리하여 master에 병합한다.
    - PR의 제목으로 된  log가 master에 병합된다.

* 되돌리기
  * Revert를 누르면 PR의 모든 commit이 되돌려진다.

* [Link](https://brunch.co.kr/@anonymdevoo/9)



<br/>

## Branch

* 일반적으로 master에 브랜치를 최종 버전으로 서비스를 배포하므로 master와 격리된 공간에서 작업하고 master에는 커밋하지 않는다.

```
- git branch <name> 
  : 현재 branch에서 새로운 브랜치를 만든다. (-b 옵션은 만들고 브랜치로 이동)
- git checkout <name>
  : <name> branch로 이동한다.
- git clone -b <branch> --single-branch <url> [dest-floder-path]
  : 특정 branch clone
```

* branch의 작업내용 병합하기
  * Merge: 베이스 branch의 head를 대상 branch의 head로 이동하는 방식
  * Rebase: rebase 했을 때의 branch head를 기준으로 재정렬?
* [Merge와 Rebase의 차이](https://brunch.co.kr/@anonymdevoo/7)
* [Link](https://brunch.co.kr/@anonymdevoo/6)



<br/>

## 되돌리기 (Reset, Revert)

* Reset (삭제) : 커밋 로그 제거

  * Commit을 되돌리기 전에 다른 사람이 Pull을 했다면, 그 사람의 Local 저장소에는 Reset하기 이전의 작업들이 존재하게 된다.
  * 나 혼자만 사용하는 브랜치에 커밋을 push한 경우에 사용
  * 되돌린 커밋을 가져간 사람이 없는 것이 확인된 경우에 사용

  ```
  1) git reset [option] HEAD~[개수]
  2) git push -f origin <branch>
  ```

* Revert (되돌리기) : 커밋 로그 남김

  * 특정 커밋으로 되돌리는 작업을 하나의 커밋으로 간주하여 커밋 log에 추가한다.

  ```
  - git revert [commit hash]
    : 한 번당 하나의 커밋 log가 생김.
  - git revert --no-commit [commit hash] 
    : working tree와 staging area에만 변경사항이 적용됨
  - git revert [--no-commit] [되돌리고 싶은 개수]
    : 복수 개의 커밋을 되돌릴 수 있다.
    	ex) git revert --no-commit HEAD~3..  # master~3..master
  ```

* 인자

  ```
  - HEAD^ : 최종 커밋 취소. 파일은 그대로.
  - HEAD~n : 마지막 n개의 커밋을 취소함
  - --hard HEAD(^|~n) : 최종 커밋 취소하고, 파일 내용도 이전으로 되돌림.
  ```

* [Link](https://jupiny.com/2019/03/19/revert-commits-in-remote-repository/)



<br/>

## Fork repository 최신 버전으로 유지하기

1. 새롭게 Fork

2. Upstream 이용 (upstream: 원본 소스코드가 있는 위치)

   ```
   1) git remote -v origin [source url] (fetch|push) # Fork
   2) git remote add upstream [source url]			  # upstream 등록
   3) git remote -v								  # 확인
   4) git fetch upstream							  # 동기화
   5) git merge upstream/master					  # 내 저장소에 merge
   
   - git remote remove upstream					  # upstream 제거
   ```

* [Link](https://jybaek.tistory.com/775)

<br/>
## git auto login on ubuntu
1. ~/.ssh 에서 ```ssh-keygen -t rsa```명령어로 ssh키 생성
2. github 홈페이지 계정설정에서 new sshkey 선택
3. 1에서 만든 id_rsa.pub 내용을 붙여넣기
4. repository에서 code ssh url 복사하기 
5. local repository에서 ```git remote set-url oigin [ssh-url]```실행
* [link](https://proni.tistory.com/entry/%F0%9F%90%A7-Ubuntu-Git-username-password-%EC%97%86%EC%9D%B4-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

<br/>

## 명명 규칙

```
https://rumblefish.tistory.com/65
개인 프로젝트를 진행할 때의 브랜치 명명규칙

https://github.com/Mash-Up-MapC/MapC-backend/
https://github.com/Mash-Up-MapC/MapC-backend/wiki/API-Endpoint-%EC%A0%95%EB%A6%AC
개발 방법, 규칙

https://github.com/mash-up-kr/9tique-android/wiki/2.-Git
Git 규칙

https://github.com/subinio/Git-GitHub-Practice/issues/1
프로젝트 수행 시 필요한 규칙
```
