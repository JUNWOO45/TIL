# REST APIs parameters

4가지 종류가 있다.

- Header parameters
- Path parameters
- Query string parameters
- Request body parameters



## Header parameters

리퀘스트 헤더 안에 포함되어있다. 주로 인증에 사용된다.

## Path paramters

엔드포인트의 일부분으로 이해하면 된다.

아래 엔드포인트에서 `{userId}` 와 `{itemId} 이다.

```
/service/user/{userId}/item/{itemId}
```

## Query string parameters

쿼리스트링 파라미터는 엔드포인트의 물음표 뒤에 온다.

각각의 쿼리 스트링 파라미터는 엠퍼센드(&)로 구분한다.

순서는 중요하지 않다.

```
/service/kakaotalk?time=1400&order=1&days=5
```

## Request body parameters

주로 POST 요청을 할 때, JSON 객체를 리퀘스트 바디 안에 넣고 보내게 된다.

```json
{
  "total": 2,
  "data": [
    {
      "id": 1,
      "name": "a1"
    },
    {
      "id": 2,
      "name": "b2"
    }
  ]
}
```



