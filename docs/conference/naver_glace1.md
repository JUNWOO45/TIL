# 지도 서비스 - 신재경

vector뷰로의 전환 준비
2017년까지는 현대??의 서비스를 사용했었음.
이젠 자체서비스.

대중교통의 서비스화의 어려움. 
자주바뀜.

"지도개발은 매우 넓은 커버리지의 기술을 필요로합니다."

최신성유지.

굉장히 많은 개발자와의 ㅎ렵업.

앵귤러기반에서 리액트기반으로.
metal/vulkan ??



# 네이버지도 API 지도검색 - 요람에서 무덤까지

##무슨이야기를 할건데?

- api개발 과정에 대한 이야기들
- 누군가에게는 도움이 될 이야기

##api lifecycle

1. planning and designing
2. developing
3. testing
4.deploying
5.retiring

##1.디자인단계
###개발스텍 결정.

- mainstream 
 java,mysql...
- challenger / legacy
node, go, mongodb, cassandra,apache...

"이러이러하기때문에 몽고디비가 프로젝트에게는 적합할 것 같습니다." 라고 할 줄 알아야함. 정답은 없음.
"대세가 그러니깐요."가 아닌, 설득,토론 문화.

###인프라스트럭쳐 infrastructure 결정.

- reliability: fault tolerance

- scalability: scale up vs scale out
- message platform

### naming

```
와 이런 고수분들도 작명이 어렵다고 하시는구나.
```

팀웍이 중요함.

협의, 토론의 문화.



## 2.development

- 기획 설계 이후, 뼈대 만들기

기획이 완벽하다는 생각은 안함.

- hello world를 작게 만들기.

- 혼자 일하는 것이 아닌, git flow를 사용함.

feature단위로 작게 쪼개서.

코드리뷰.(온라인/ 오프라인)

- ci/cd

젠킨스, 웹후드? 깃헙 엔터프라이즈를 쓰기때문에 사용하신다고함.

- 개발 스프린트는 짧게는 2주, 길게는 4주까지



## 3. 테스트

- QA

- Regression Test : 배포 직전의 스테이지단계에서 프로덕션 로그 기반의 테스트.

- Performance Test : github.com/naver/ngrinder 를 사용함.

  ```
  오 이게 뭐지!?!?!? 내일 알아보자.
  ```

- 가용량 점검, 증설.



## 4. deploy

- load balance
  - 필수
- Blue/Green deploy
  - 컨테이너 기반의 서비스에대해서는 도입.
  - 블루와 그린 두군데에 트래픽이 분산되다가 결국에는 그린으로 트래픽 완전이전
- a/b test (sprint clodu config)
- 배포한 이후 에는 다음과 같은 일을 해요.
  - 서버 모니터링: cpu, memory, filesystem, io등등 nagios, zabbix, prometheus in k8s
  - api monitoring (tps, error logging): github.com/naver/pinpoint
  - collect logs: elk, ga, firebase
  - data analysis : apache spark



## 5.retirement?

nope.

지도 api에는 리타이어먼트가 없음.ㅎㅎ

ㅈㅣ도앱이 v5가 나와도 v4를 사용하는사람들이 많음.



---

코드를 보여줘라.

커밋의 중요성.

의미있게. "이렇게 코딩하고있어요."

필요하다면 커밋히스토리, PR도 확인한다.

오픈소스도 좋게봄.

---

# 네이버 지도앱은 다른 앱과 이런게 다릅니다. - 김창기



벡터맵 sdk, 네비게이션 sdk, ios, 안드로이드 4가지 작업을 같이 하고 있습니다.

