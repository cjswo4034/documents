# IntelliJ IDEA 팁

### **Jetbrain toolbox** 

- jetbrain 관련 툴을 한눈에 보고 관리 가능



### **JIRA**

- Preference > Tools > Tasks > Servers > jira 서버 추가

  * alt + shift + n

  - 나의 jira 선택가능
  - jira에 대한 progress를 선택, 브랜치 생성 등 가능
- [Link] (https://jojoldu.tistory.com/260)



### Git

- Git flow 관련해서 필요한 것들을 intellij 내부에서 자동으로 처리 가능(ex. develop에서 feature 따기)

- Preference > Plugin > Git Flow integration 설치

- JIRA 관련 task 진행

  - Gitflow operation

    * Git flow 버젼에 맞는 feature, hotfix 브랜치가 자동으로 만들어짐(브랜치 이름도 jira 번호가 자동 입력됨)

    - 코드수정

    - **commit 하게 되면 자동으로 message가 템플릿으로 만들어짐**, 변경가능

      ​	Preference > Tools > Tasks > Servers > Commit Message 에서 수정가능

  - task finish 

    * Gitflow 전략에 따라 **자동으로 feature브랜치가 develop브랜치로 머지**가 됨




### **UPSOURCE** ([Link](https://jojoldu.tistory.com/258?category=678716))

- 회사에 남는 서버에 java8과 같이 깔아서 씀.
  - **local의 intellij와 연동되면서 pull request에 대한 메시지들이 push message**처럼 나오게됨.



###  Database

- intellij가 깔리는 곳에는 모든 database를 사용가능함.(ex. 특히 oracle)
- h2도 사용가능함
- cmd + d : create duplicate code(auto copy+paste)



### JSON

- api json formatting기능
- **json 정렬필요하다면?**
- json viewer
- **json으로 DTO 만들고 싶다면?**
  - class 새로만들어서 우클릭 -> make class(getter setter 가능)
- **class를 json형태로 만들고 싶다면?**
  - class 에서 우클릭 -> make json
- **json을 string type으로 하고싶다면?**
  - alt + enter : 어떤 형태로 입력할것인가? -> json 선택
  - Json입력



###  번역

- Translator jojoldu: (번역 plugin)
- alt + 1 : 변수를 번역해줌



### 커맨드

- 이동 및 탐색
  - 전체 검색: `Shift + Shift`
  - Action 검색: `shift + ctrl + a`
  - 프로젝트에서 코드 검색 : `Shift + Ctrl + F`

* 라인 
  * 복사 :  `Ctrl + D`
  * 삭제 :  `Ctrl + y`
  * 오리기 :  `Ctrl + x`
  * 합치기 :  `Ctrl + Shift + j ` (밑에 있는 줄을 현재 줄의 맨 뒤로 합침)
  * 옮기기 1 :  `Shift + Alt + (Up | Down)` (구문, 문법 신경쓰지 않고 옮김)
  * 옮기기 2 :  `Shift + Ctrl + (Up | Down)` (문법적 오류 한도 내에서 옮길 수 있음)



* 구문

  * 구문 옮기기 :  `Shift + Ctrl + Alt + (Left | Down)` 

    > 매개변수 or 태그 등의 구문을 좌, 우로 이동

  * 