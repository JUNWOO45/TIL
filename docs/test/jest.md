# Jest란

---

정리하기에 앞서, 조사하면서 읽은 좋은 글들을 먼저 공유합니다.

[[8퍼센트 블로그] 코드 커버리지 80% 넘긴 썰](https://brunch.co.kr/@leehosung/43)

[TOAST UI 테스트](https://ui.toast.com/fe-guide/ko_TEST/#jest)

[Python 테스트 시작하기](https://www.slideshare.net/hosunglee948/python-52222334)



---



굉장히 많이 사용되는, 페이스북에서 만든 테스트 프레임워크입니다.

많은 장점과 유용한 기능들을 가지고 있습니다.

## 쉬운 설치 및 실행

Jest는 테스트 러너의 기능 뿐 아니라, 단언, 테스트 더블, 코드 커버리지 등 테스트에 필요한 많은 기능들을 지원하기 때문에 별도의 추가 설치가 필요 없습니다.

npm 명령어로 설치합니다.

```
$ npm i --save-dev jest
```

실행을 돕기위해 `package.json` 에 스크립트를 등록합니다.

```
{ 
	// ...
	"test": "jest"
}
```

테스트파일이 `*.test.js` 형식이라면, 추가 설정 없이 바로 실행할 수 있습니다.

```
$ npm test
```



<br>

## 쉬운 커버리지 측정

`--coverage` 옵션만 추가해서 커맨드 라인을 실행해주면 끝납니다.

```
$ npm test -- --coverage
//또는

$ jest --coverage
```

![jest1](/Users/ns/Documents/works/fe-study/parkjunwoo/pic/jest1.png)



<br>

## jsdom 내장

노드js환경에서는 브라우저에서 제공하는 DOM이나 window객체를 사용할 수 없습니다.

이러한 API를 사용할 수 있는 가상환경을 구성해주어야하는데, jest는 jsdom을 내장하고 있습니다.

<br>

## 스냅샷 테스트

객체 내부의 상태를 그대로 파일로 저장해 놓고, 다음 테스트에서 객체의 현재 상태가 이전에 저장된 상태와 다른지를 비교하는 테스트입니다.



---

### afterEach()

```javascript
// 각 테스트를 실행 후, 저장되어 있는 데이터를 정리해주는 작업이 필요하다.
// afterEach가 유용하다.
afterEach(() => {
  data.users.splice(0);
})
```

<br>

### beforeEach()

```javascript
// 테스트마다 실행되는 중복되는 코드들을 빼낼 수 있다.
beforeEach(() => {
	data.users.push({
    id: 1,
    name: 'User1',
    email: 'User1@test.com'
  },
  {
    id: 2,
    name: 'User2',
    email: 'User2@test.com'
  },
  {
    id: 3,
    name: 'User3',
    email: 'User3@test.com'
  });
});

```

<br>

### beforeAll(), afterAll()

테스트 함수 각각의 전, 후에 호출되는 것이 아니라, 맨 처음과 맨 끝에 단 한 번만 호출된다.

DB에 접속하는 경우에 사용할 수 있을 것 같다.

연결하고, 연결을 끊고.

---

### only(), skip()

수 많은 테스트 함수 중, 하나만 실패했을 경우 해당 테스트만 실행해보고 싶을 때 사용한다.

```javascript
test.only('run only...', () => {
  // 이 테스트 함수만 실행된다.
})
```

반대로, 해당 함수를 스킵할 수도 있다.

```javascript
test.skip('이 함수는 스킵됩니다!', () => {
  // skip..
});
```

<br>

### 그 외 [matchers](https://jestjs.io/docs/en/using-matchers)

