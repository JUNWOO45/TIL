## Git-flow 전략이란?

Git-flow에는 5가지 종류의 브랜치가 존재합니다.

항상 유지되는 메인 브랜치들(master, develop)과 일정 기간 동안만 유지되는 보조 브랜치들(feature, release, hotfix)

- master: 제품으로 출시되는 브랜치
- develop: 다음 출시 버전을 개발하는 브랜치
- feature: 기능을 개발하는 브랜치
- release: 이번 출시 버전을 준비하는 브랜치
- hotfix: 출시 버전(master)에서 발생한 버그를 수정하는 브랜치

![git-flow](../pic/git-flow.png)



설명을 해보면..

우선, 태초의 master브랜치가 있을겁니다. 

그리고 이 master브랜치에서 생성된 develop브랜치가 존재합니다.

이 두 브랜치는 항상 존재하게 됩니다.

develop브랜치에서는 버그를 수정한 커밋들이 계속 추가됩니다.

이 develop브랜치에 새로운 기능을 추가시키고 싶으면, develop브랜치에서 feature브랜치를 생성시킵니다.

기능 추가 개발이 완료되면, feature 브랜치는 develop 브랜치로 merge됩니다.

이번 버전에서 개발될 작업들이 모두 완료되면, develop브랜치에서 release브랜치를 생성합니다.

release브랜치에서는 QA가 이루어 집니다!

이 QA에서 발견된 버그들은 release브랜치 자체에서 수정되고 커밋됩니다.

QA가 모두 통과되었다면, release브랜치를 master와 develop 브랜치로 merge합니다.

---

## poor side of git-flow



### 1. teams do not finish their jobvs at the same time.

계획된 release들은 이론상으로는 좋다. 하지만 실제는 다르다.

### 2. you cant know for sure that only those planned features need to go live.

계획된 요청사항이 전부가 아니다.애자일한 상황에서는 더더욱.

### 3. features are assumed to be independent of each other, which are not.

사실상 git-flow는 독립적인 작업들을 가정하고 있는데 사실상 그렇지 못하다. 

```
poor side 출처 : http://luci.criosweb.ro/a-real-life-git-workflow-why-git-flow-does-not-work-for-us/
```

