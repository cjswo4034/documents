# Ubuntu 팁

## 환경변수 설정

1. alias 명령어로 변수 만들기

    ```shell
    1) sed -i '$aalias [변수명]="명령어"' ~/.zshrc
    2) source ~/.zshrc
    ```

   - trello 관련 변수
     - trcs : google-chrome https://trello.com/b/KTftSr0P/cs
     - trlog : google-chrome https://trello.com/b/zg7FpuoX/devlog
   - idea 관련 변수
     - idlog : idea.sh ~/nsm/project/devlog
     - iddoc : idea.sh ~/nsm/project/devlog
     - idjava : idea.sh ~/nsm/project/devlog
   - 기타
     - ws : cd ~/nsm/project

2. 환경변수 만들기
  
   - z쉘이 설정을 불러오는 순서 ([링크](https://wiki.archlinux.org/index.php/zsh#Startup.2FShutdown_files))
     1. zshenv
     2. zprofile
     3. zshrc
     4. zlogin

<br>

## Git username, password 없이 사용하기

1. 우분투에서 공개키 만들기 ([출처](https://proni.tistory.com/entry/%F0%9F%90%A7-Ubuntu-Git-username-password-%EC%97%86%EC%9D%B4-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0))

    ```shell
    ssh-keygen -t rsa [-b bitsize]
    a) 공개키를 생성할 경로를 지정한다. 엔터치면 기본 경로에 만든다.
    b) 공개키를 사용할 때 묻는 비밀번호로 권장값은 10~30의 문자이고 생략가능하다.
    c) 비밀번호를 확인하는 단계로 b)에서 입력한 값을 입력한다.
    ```

    > 보안을 위해서 공개키를 만들고 chmod로 권한을 수정해야한다.
    >
    > 개인키 : ~/.ssh/id_rsa
    >
    > 공개키 : ~/.ssh/id_rsa.pub

2. git에서 ssh키 등록하기

   1. git 홈페이지에서 `Profile -> Setting -> SSH and GPG keys`탭으로 이동
   2. `New SSH key`를 클릭하고 Title과 Key 입력해서 SSH key를 등록한다.

        - Title은 아무거나 입력한다.
        - Key에는 1.에서 만든 공개키를 입력한다.

3. remote repository url 변경하기

   1. git의 project page에서 `use url`을 클릭한 다음 링크를 복사한다.

        ![ssh](../images/ssh_url.png)

   2. local repository의 루트에서 터미널을 열고 다음 명령을 실행한다.

        ```shell
        git remote set-url origin [ssh url]  # (clone한 경우)
        git clone [ssh url]                  # (clone하지 않은 경우)
        ```

   3. 비밀번호를 묻는다면 공개키를 만들 때 입력했던 passphrase값을 입력한다.



## 브라우저에서 휠 버튼 클릭시 스크롤이 안될 때

1. 마우스의 deviceID를 찾기

   ```shell
   xinput list | grep -i mouse
   ```

   

2. 마우스의 옵션 중 scroll method id 찾기

   ```shell
   xinput --list-props <deviceId> | grep -i scroll
   ```

   man libinput을 보면 scroll method는 어떤 방법을 사용했을 때 스크롤 동작을 할 것인지 묻는 속성. 3번째가 버튼이라 3번째에 값 1을 줘야됨.

   button scrolling button은 1: 왼쪽, 2: 중앙, 3:오른쪽 버튼을 의미하며 스크롤 메소드는 이 옵션에 지정된 버튼이 메소드에 지정된 방법으로 눌렸을 때 동작.

   

3. Scroll Method Enabled 속성의 값을 0, 0, 1로 설정

   ```shell
   xinput set-prop <deviceId> "libinput Scroll Method Enabled" 0, 0, 1
   ```

   

4. 부팅 시 자동으로 설정

   ```shell
   echo 'xinput set-prop <deviceId> "libinput Scroll Method Enabled" 0, 0, 1' >> .xinpurc
   ```

   > 모든 유저에게 적용하려면 



- References
  - [askubuntu](https://askubuntu.com/questions/20298/how-to-make-xinput-settings-persist-after-devices-are-unplugged-replugged-and/461173#461173)
  - [man page](http://manpages.ubuntu.com/manpages/bionic/man4/libinput.4.html)



<br>



## 테마 관련

### 폴더 사이드바의 별표 추가하기

* 파일이나 폴더를 오른쪽 클릭했을 때 나타나는 '별표 붙이기' 항목을 통해 별표를 붙일 수 있다.
* 책갈피가 되어있으면서, 설정 -> 검색 -> 검색 위치 -> 책갈피 탭에서 옵션이 활성화 되어있는 폴더의 하위 파일이나 폴더에만 '별표 붙이기'를 할 수 있다.
* 별표가 붙은 항목은 사이드바의 별표 탭에서 확인할 수 있다.



- 아래의 상황에서는 별표 붙이기 항목이 나타나서 별표를 붙이더라도 동작하지 않는다.

  1. 현재 폴더를 책갈피에 등록한다.
  2. 현재 폴더를 검색가능하게 변경한다.
  3. 책갈피를 제거한다.

  > 위와 같이 검색 가능하지만 책갈피가 아닌 폴더 내의 파일이나 폴더는 별표 붙이기 항목이 나타나긴 하지만 별표를 붙여도 아무 변화가 없다.



### 폴더 사이드바의 어플리케이션 지우기 or 연결 디렉토리 변경하기

* xdg-user-dirs-update 명령어로 /etc/xdg/user-dirs.defaults 에서 기본값 읽음
* /etc/xdg/user-dirs.conf 에서 설정함. 유저 홈 디렉토리의 ~/.config/user-dirs.conf가 있으면 유저 홈의 conf파일의 우선순위가 높음
* 유저 초기화할 때 conf 읽고 defaults에 있는 Key값과 매칭되는 value를 홈 디렉토리에서 찾고 user-dirs.dirs를 매핑시킴
* 사이드바에서 보기 싫은 디렉토리를 .defaults 파일에서 #으로 주석처리한다.



### 동작과정 [링크](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html)

1. /usr/share/applications/nautilus-autorun-software.desktop 
2. 1의 exec인 nautilus-autorun-software 실행



<br>

## 기타

### 명령어

- deb파일 설치하기 : `sudo dpkg -i (deb file)`

### 커맨드

- 터미널
  - 터미널 열기 : `ctrl + alt + t`
- 애플리케이션
  - 전체 목록 열기 : `super + a`
