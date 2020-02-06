# 개발 환경 설정



## iTerm2

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

