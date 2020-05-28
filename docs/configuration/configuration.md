# 개발 환경 설정

## Mac

### 환경설정 > 트랙패드

- 탭하여 클릭하기
- 추가 제스처 네 손가락 설정

### 환경설정 > 손쉬운 사용 > 포인터 제어기 > 트랙패드 옵션 > 드래그 활성화 "세 손가락으로"



### 환경설정 > 디스플레이 > 정렬

- 모니터에 맞춰서 정렬..

### 환경설정 > 데스크탑 및 화면보호기 > 핫코너

- 왼쪽 상단: 잠금화면

### 환경설정 > Dock

- 자동으로 Dock 가리기와 보기
- Dock 나타나는 애니메이션 삭제하여 반응성 향상
  터미널 열고 아래 명령어 실행

```
defaults write com.apple.dock autohide -bool true && defaults write com.apple.dock autohide-delay -float 0 && defaults write com.apple.dock autohide-time-modifier -float 0 && killall Dock
```



## iTerm2

### 1-0 설치

[https://www.iterm2.com/](https://www.iterm2.com/)

### 1-1 brew설치

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 1-2 zsh 설치

```
brew install zsh
```

### 1-3 oh my ZSH 설치

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### 1-4 agnoster 테마 설치

```
vim ~/.zshrc

ZSH_THEME="robyrussell" -> ZSH_THEME="agnoster"
```

### 1-5 폰트 변경

[https://github.com/naver/d2codingfont](https://github.com/naver/d2codingfont) 들어가서 폰트 다운로드

압축풀고 폰트 더블클릭 후, '서체 설치' 눌러서 설치.

참고 : [https://m.blog.naver.com/PostView.nhn?blogId=lxxjxxx&logNo=221181233993&proxyReferer=https:%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=lxxjxxx&logNo=221181233993&proxyReferer=https:%2F%2Fwww.google.com%2F)

Preference > Profile > Text에서 D2Coding폰트 적용 및 13pt로 폰트크기 변경

### 1-6 macbook-pro부분 삭제

```
vim ~/.zshrc
```

들어가서,

```
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
  fi
}
```

복붙 후 저장.

<br>

---

### - command + 좌우화살표 / option + 좌우화살표로 단어 사이 옮겨다니기

```
iTerm2 -> Preferences -> Profiles -> Keys -> Presets.. -> Natural text editing
```



### - zsh 조금 더 이쁘게 꾸미기

zshrc를 열어준다.

```
vim ~/.zshrc
```

파일 하단에 아래 코드를 복붙

```
prompt_context() { # Custom (Random emoji) emojis=("⚡️" "🔥" "🇰" "👑" "😎" "🐸" "🐵"  "🌈" "🍻" "🚀" "💡" "🎉" "🔑" "🚦" "🌙") RAND_EMOJI_N=$(( $RANDOM % ${#emojis[@]} + 1)) prompt_segment black default "{하고싶은이름} ${emojis[$RAND_EMOJI_N]} " }
```



Reference: https://fernando.kr/15?category=790197

---

## Git

### - 커밋 메세지 템플릿 



우선, 가이드대로 `~/.gitmessage.txt` 파일을 만들어주고, 에디터로 진입.

```
touch ~/.gitmessage.txt
nano .gitmessate.txt
```

아래 커스텀 템플릿을 복붙해주고 저장.

```
# <타입>: <제목>

##### 제목은 최대 50 글자까지만 입력 ############## -> |


# 본문은 위에 작성
######## 본문은 한 줄에 최대 72 글자까지만 입력 ########################### -> |

# 꼬릿말은 아래에 작성: ex) #이슈 번호

# --- COMMIT END ---
# <타입> 리스트
#   feat    : 기능 (새로운 기능)
#   fix     : 버그 (버그 수정)
#   refactor: 리팩토링
#   style   : 스타일 (코드 형식, 세미콜론 추가: 비즈니스 로직에 변경 없음)
#   docs    : 문서 (문서 추가, 수정, 삭제)
#   test    : 테스트 (테스트 코드 추가, 수정, 삭제: 비즈니스 로직에 변경 없음)
#   chore   : 기타 변경사항 (빌드 스크립트 수정 등)
# ------------------
# Remember me ~
#   Capitalize the subject line
#   	제목 첫 글자를 대문자로
#   Use the imperative mood in the subject line
#     제목은 명령문으로
#   Do not end the subject line with a period
#     제목 끝에 마침표(.) 금지
#   Separate subject from body with a blank line
#     제목과 본문을 한 줄 띄워 분리하기
#   Use the body to explain what and why vs. how
#     본문은 "어떻게" 보다 "무엇을", "왜"를 설명한다.
#   Can use multiple lines with "-" for bullet points in body
#     본문에 여러줄의 메시지를 작성할 땐 "-"로 구분
# ------------------
```

그리고 `git commit.template` 에 이 파일을 설정해준다.

```
git config --global commit.template ~/.gitmessage.txt
```

Reference

- [https://git-scm.com/book/ko/v2/Git%EB%A7%9E%EC%B6%A4-Git-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0](https://git-scm.com/book/ko/v2/Git맞춤-Git-설정하기)



---

## VSCode

### code . 적용

```
Shift + Command +  P and type `shell command`
```



