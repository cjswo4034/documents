# Convention

## Git Planing

### Branch

- `Master` : Release 완료한 버전을 merge 하고, Release 완료 시 Tag를 함께 둔다.
- `Develop` : Master Branch 기준으로 티켓 단위 개발 작업을 진행하며, 필요에 따라서 타 Develop Branch를 Merge 한다.
- `Release` : 릴리즈 플래닝이 끝나면 작업 완료한 티켓을 머지 한다.
- `HotFix`
  - 긴급 수정 브랜치
  - 시작 브랜치: `master`
  - 종료 브랜치: `master`, `develop`
  - `hotfix/{내용}`
- `Feature`
  - 기능을 개발할 때 사용하는 브렌치
  - 브랜치 뒤에 생성날짜 넣기
  - 시작 브랜치: `develop`
  - 병합 브랜치: `develop`
  - `feature/{기능 이름}_20201010`

## Commit Guidline [[link](https://gist.github.com/abravalheri/34aeb7b18d61392251a2)]

- type(scope): subject meta
- commitlint를 사용해서 커밋 검사.
- 본문은 what do why 형식으로 작성.

- type
  - add : 정적 파일, 디렉토리, 설정 파일 등이 추가되었을 때
  - feat : 새로운 기능 추가
  - fix : 버그 & 오류 & 오탈자 수정
  - docs : 문서를 수정한 경우
  - refact : 코드 리펙토링
  - test : 테스트를 추가하거나 수정한 경우
  - perf : 성능 개선을 위해 코드를 변경한 경우
  - build : 빌드 시스템이나 의존성을 추가한 경우
  - chore : (로직의 큰 변경 없이) 잡다한 수정
  - style : (로직의 변경 없이) 스타일만 변경한 경우 (들여쓰기, 세미콜론 등)

- scope
  - 커밋의 대상이 되는 것을 명시
  - 페이지 또는 모듈이나 기능 단위로 제한함
  - `feat(auth): introduce sign in via Facebook`

- subject
  - 변경사항을 간결하게 기술
  - 마침표를 찍지 않고 What to do 위주로 작성.

### Issue

- 문제가 생긴 사항을 간결하게 기술
- 관련된 범위에 대한 태그 넣기
  - backend
  - frontend
  - test
  - environment
  - document

### Pull Request

- Title
  - [branch] {task 번호} [PR 내용 요약(feature)]
- Contents
  - 개발한 기능
  - 변경사항 및 이유
  - 헷갈리는 부분
  - 참고

## Coding Convention

- lint, Prettier 사용하기

  ```text
  lint - node.js: ESLint, Typescript: tslint, Python: Pylint, Java: sonarlint (SonarQube와 연동)

  ```

- Naming
  - 메소드명은 `동사 + 목적어`
  - 변수명은 `명사`
  - css 변수명 사이의 공백은 `-`로 처리
  - 약어
    - image -> img
    - check -> chk
    - description -> desc
    - value -> val
    - count -> cnt
    - number -> num
    - purchase -> buy

- Code
  - 메소드 파라미터가 3개 이상이면 객체로 감싸서 넘기기
  - 메소드는 간결하게 (10줄 이내 권장)
  - 다중 반복문이 되면 메소드로 분리하기
  - 매직넘버, 절대값 없애기
