<h1>
  git reflog
</h1>





<h2>git reflog명령을 이용하면 hard-reset을 되돌릴 수 있다!</h2>



```
HEAD
- 마지막 커밋의 참조
- 가장 최신 커밋
- 혹은 새로운 커밋의 부모
```

```
git reset
- HEAD의 상태를 변경시키는 명령
- 옵션에 따라 HEAD, 스테이지, 작업 디렉토리의 내용이 달라짐
- 보통 강제로 특정 커밋으로 돌아가고 싶을 때 많이 사용함.
```



```
$ git log --oneline
- git log를 한줄로 볼때!
```

```
$ git reset --hard HEAD~
- 커밋 하나 전으로 돌아가기
```

```
3477df6 (HEAD -> master) commit 2
b6596fc commit 1
7e5b465 (origin/master, origin/HEAD) Initial commit
```

```
실수로 3477df6까지 $ git reset --hard HEAD로 지워버려서,
b6596fc (HEAD -> master)가 되어버렸다면,,,,

$ git reset --hard 3477df6
로 되돌릴 수 있다!!
```

```
하지만 이걸 기억하고 있는 사람이 있을 수 없으니........
그 해결책은 바로
$ git reflog
```

```
$ git reflog로 나오는 모든 커밋로그를 확인한 후 ID를 가지고 쉽게 되돌릴 수 있다..
```

```
$ git reflog
- 참조(reference)의 기록(log)를 보여주는 명령
- hard reset을 되돌릴 수 있다!
```

```
- Git의 커밋은 "세이브포인트"랑 같다!~
- git reflog명령을 이용하면 hard-reset도 되돌릴 수 있다!
- 거의 모든 상황에서 커밋은 복구될 수 있다!
```

