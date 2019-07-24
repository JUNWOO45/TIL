#gcloud deploy



굉장히 의미없는 기록일 수 있는데 굉장히 어려워서 이렇게라도 적어놓음..

## 1. 우선 build.

다만 지금 내가 하는 build는 production모드가 아니라 develop모드.

## 2. deploy

```
$ cd static
$ gcloud app deploy -v qa --quiet
```



## 진행하면서 알게된점

- app.yaml이 필요한 것.

- 그리고 package.json의 main값인 server.js의 존재.

- gcloud platform > 서비스 > 디스패치.

  요 dispatch가 정확히 어떤식으로 작동하는지느 ㄴ모르겠지만 토이프로젝트만들때 라우터와 비슷하게 동작하는듯.ㅇㅇ..

  요 dispatch는 dispatch.yaml으로 설정해주는데 이게 좀 알쏭달쏭하네.

  ```
  $ gcloud app deploy dispath.yaml
  ```

  명령어로 dispatch.yaml을 등록 가능함.

  dispatch.yaml 수정 후 등록하니깐 console에서 보이는 dispatch 수정되네.