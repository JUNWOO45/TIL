add

```
git add [file name]
```



모든 파일 add

```
git add *
```



commit

```
git commit -m "[message]"
```



add + commit

```
git commit -am "[message]"
```



branch 생성

```
git checkout -b [branch name]
```



branch이름 바꾸기

```
git branch -M [change name]
```



특정 branch에 push하기

```
git push origin [branch name]
```



branch간 이동하기

```
git checkout [branch name]
```



commit log 확인

```
git log
```



<hr>

변경이력이 있는 파일 변경사항 취소

```
git checkout -- [file name]
```



바로 직전 commit message 수정

```
git commit --amend
```



commit한개 취소

```
git reset HEAD^

git revert HEAD
```



현재 branch의 변경사항을 커밋없이 저장해두기

```
git stash
```



stash로 저장해둔 변경 내역 불러오기

```
git stash pop
```



다른 banch의 특정 commit을 가져와서 merge하기

```
git cherry-pick [commit hash number]
```



<hr>

git log 시각화

1.

```
$ open ~/.gitconfig
```

2.

```
[alias]
        lg1 = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
        lg1a = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%x09%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
        lg2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
        lg3 = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset)%C(bold yellow)%d%C(reset) %C(white)%s%C(reset) %C(bold green)(%ar)%C(reset) %C(dim white)- %an%C(reset)' --all
        lg4 = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset)%C(bold yellow)%d%C(reset) %C(white)%s%C(reset) %C(bold green)(%ar)%C(reset) %C(dim white)- %an%C(reset)'
        lg = !"git lg4"
        lga = !"git lg3"
        st = status
        co = checkout
        nb = checkout -b
        com = checkout master
        po = push origin
```

3.

```
git lg
git lg1
git lg2
git lg3
```



<hr>



