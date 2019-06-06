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


```
$ git rm --cached [파일명]
- 원격저장소의 파일만 삭제하고, 로컬저장소의 파일은 그대로 둔다.
```


