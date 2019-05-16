<h1>
  DATABASE를 다루면서 생긴 ERROR
</h1>

<hr>

로컬에서 database를 불러오려고 할때마다, 에러가뜨면서 데이터를 읽을 수가 없었습니다.

```
1449, u"The user specified as a definer ('root'@'%') does not exist")
```

해결법:

Data가 있는 폴더에 들어가서..

```
Mac
sed -i '' 's/DEFINER=`root`@`%`//g' [DB_FILE_NAME].sql
```

또는 텍스트에디터로 관련 문자열을 삭제해주면 해결된다고 합니다..

<hr>