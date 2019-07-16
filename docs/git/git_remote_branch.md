## Git remote branch 가져오기

원격 저장소의 브랜치를 가져와서 작업해야하는 경우가 자주 있는데요.

정리해보려 합니다.

- git remote를 갱신해줘야 합니다.

```
$ git remote update
```

- 원격 저장소 branch 확인

  `$ git branch -r` -r옵션으로 원격 저장소의 branch list를 볼 수 있습니다.

  `$ git branch -a`-a옵션으로 로컬과 원격 저장소 모두의 branch list를 볼 수 있습니다.

```
$ git branch -r
```

- 원격 저장소의 branch 가져오기

  `$ git checkout -t` 를 사용해서 가져올 수 있는데요.

  예를 들어, feature/summer_vacation이라는 원격브랜치를 가져오고싶다면

```
$ git checkout -t origin/feature/summer_vacation
```

