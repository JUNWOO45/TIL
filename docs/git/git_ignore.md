# Git ignore

매번 gcloud app deploy를 할때마다....

```git
ERROR: (gcloud.app.deploy) The [version] field is specified in file [/...../app.yaml]. This field is not used by gcloud and must be removed. Versions are generated automatically by default but can also be manually specified by setting the `--version` flag on individual command executions.
```

오류가 떴었습니다.

https://stackoverflow.com/questions/43512630/gcloud-app-deploy-command-not-working

여기를 참고해서 항상 app.yaml에서 version을 주석처리를 했었는데 까먹고 주석을 안풀고 commit하는 불상사가 자꾸..........



.gitignore에 추가하려고 하는데 이티님께서 엄청 좋은 링크를 보내주셨습니다...!

https://wildlyinaccurate.com/git-ignore-changes-in-already-tracked-files/



요약하자면, .gitignore에 등록해도 이미 tracked된 파일을 계속 추적하려하기때문에 한번더 작업해야하므로 

```
$ git update-index --assume-unchanged <file>
```

를 사용하는게 더 easy하다..! 정도가 되겠네요.

```
$ git update-index --no-assume-unchanged <file>
```

를 입력하면 다시 tracking changes할 수 있습니다.



---

## How to make Git forget a file was tracked but is now in .girignore?

git은 already being tracked된 파일들을 계속해서 추적하려고해서, 뒤늦게 .gitignore에 등록한다해도 계속 해당 파일을 추적하려합니다.

따라서 tracing을 멈추려면....

```
$ git rm --cached <file>
```

로 파일을 지워주거나,

```
$ git rm -r --cached <folder>
```

로 폴더를 통째로 지워줘야합니다.



---

```
$ git update-index --assume-unchanged <file>
```

명령어로 임시로 변경내역에서 제외했는데, 오랜시간이 흐른뒤에 내가 뭘 변경내역에서 제외했는지 기억이 안날때는...?

```
$ git ls-files -v | grep ^h
```

를 입력하면 unchanged