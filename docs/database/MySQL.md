<h1>
  MySQL
</h1>


1. 데이터베이스(스키마)를 만들 때

2. ```
   CREATE DATABASE tutorial_database;
   ```

2. 데이터베이스(스키마)를 지울때

   ```
   DROP DATABASE tutorial_database;
   ```

3. 이 데이터베이스를 사용하겠다!

   ```
   USE tutorial_database;
   ```

4. 테이블 만들기

   ```
   CREATE TABLE topic(
     -> id INT(11) NOT NULL AUTO_INCREMENT,
     -> title VARCHAR(10) NOT NULL,
     -> description TEXT NULL,
     -> created DATETIME NOT NULL,
     -> name VARCHAR(10) NOT NULL,
     -> profile VARCHAR(50) NOT NULL,
     -> PRIMARY KEY(id)
   );
   ```

5. 테이블 확인

   ```
   SHOW tables;
   ```

6. 정렬된 순서로 보고싶을때

   ```
   DESC topic;
   ```

7. 데이터를 넣을때

   ```
   INSERT INTO topic (title, description, created, name, profile) values ('Avengers', 'hero movie', now(), 'junwoo', 'developer')
   ```

8. 이렇게 들어간 데이터를 확인하고 싶을때는

   ```
   SELECT * FROM topic;
   ```

9. 조건을 만족하는 데이터만 확인하고 싶을때는

   ```
   SELECT * FROM topic WHERE name='junwoo';
   ```

10. 순서정렬, 리미트제한등의 특별한 조건을 걸고 데이터를 확인하고 싶을때

    ```
    SELECT * FROM topic WHERE description='hero movie' ORDER BY id DESC;
    :description이 'hero movie'인 모든 데이터를 id값 내림차순으로
    
    SELECT id, title FROM topic ORDER BY description limit 2;
    
    ```

11. 업데이트

    ```
    UPDATE topic SET description='hero movie' WHERE id=1;
    ```

    타겟을 정확이 지정해주는 것이 중요.

12. 삭제

    ```
    DELETE FROM topic WHERE id=5;
    ```

    얘도 타겟을 정확히 지정해주는 것이 중요.

13. join

    ```
    SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.id;
    ```

14. join할때 유의할점

    ```
    SELECT id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;
    ```

    라고하면 에러가 발생합니다.

    ```
    ERROR 1052 (23000): Column 'id' in field list is ambiguous
    ```

    topic테이블과 author테이블 모두에 id가 있어서 모호하다고 하네요.

    이럴때는,

    ```
    SELECT topic.id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;
    ```

    로 수정해주어야합니다.

15. as

    ```
    SELECT topic.id AS topic_id, title FROM topic LEFT JOIN author ON topic.author_id = author.id;
    ```




<hr>

<h1>
  WHERE 절
</h1>



1.where 절에 들어가는 연산자

```
=, >, >=, <, <=, BETWEEN a AND b, IN(list), LIKE '비교문자열', IS NULL, AND, OR, NOT !=, ^=, <>, NOT 칼럼명 =, NOT 칼럼명 >, NOT BETWEEN a ADN b, NOT IN(list), IS NOT NULL
```

2.연산자 우선순위

```
1. 괄호()
2. NOT
3. 비교연산자
4. AND
5. OR
```

3.예제

```
SELECT player_name 선수이름, position 포지션, back_number 백넘버, height 키
FROM player
WHERE team_id = 'hello'
;
```

```
선수테이블에서 팀코드가 'hello'인 선수들의 이름, 포지션, 백넘버, 키를 가져오라는 의미.
```

4.문자 유형 비교 방법

- 비교 연산자의 양쪽 모두 CHAR타입인 경우

  ```
  1. 서로 길이가 다르면 짧은쪽에 space를 추가하여 길이를 같게 한 후에 비교.
  2. 서로 다른 문자가 나올때까지 비교
  3. 달라진 첫번째 문자의 값에따라 크기 결정
  4. BLANK의 수만 다르다면 서로 같은 값으로 인정
  ```

- 비교 연산자의 양쪽이 모두 VARCHAR타입인 경우

  ```
  1. 서로 다른 문자가 나올때까지 비교
  2. 길이가 다르다면 짧은 것이 먼저 끝날때까지만 비교 후 길이가 긴 것이 크다고 판단.
  3. 길이가 같고 다른것이 없으면 같다고 판단
  ```

5.SQL연산자

```
SELECT player_name 선수이름, position 포지션, back_number 백넘버, height 키
FROM player
WHERE team_id IN ('hello', 'hi')
;
```

```
선수테이블에서 팀코드가 'hello'나'hi'중에 있는지 판단해서 레코드를 달라는 의미.
```



```
SELECT name, job, age
FROM friends
WHERE (job, age) IN (('manager', 20), ('developer', 30));
```

```
직업이 매니저이면서 20살, 직업이 개발자이면서 30살인 친구정보를 추출
```



```
SELECT name, job, age
FROM friends
WHERE job IN ('manager', 'developer') AND age IN(20,30);
```

```
의미가 위에거랑은 다름.
직업이 매니저, 개발자 둘 중 하나이면서 나이가 20,30살인 경우 정보 추출.
즉, 매니저이면서 30살인 경우에도 조건을 충족해서 위의 SQL문과는 차이가있다.
```



```
SELECT name, job, age
FROM friends
WHERE name LIKE '박%';
```

```
이름이 박으로 시작하는 친구 추출
```

```
% : 0개 이상의 어떠한 글자.
_ : 1개인 단일 문자
```

```
예를 들어, 
WHERE name LIKE '_a%';
라면 첫번째의 어떤 단일문자가 있고, 두번째 글자가 a로시작하는 이름의 사람 추출.
```



```
SELECT name, job, age, height
FROM friends
WHERE height BETWEEN 170 AND 180;
```

```
친구들 중에서 키가 170이상, 180이하인 선수 추출
```



```
SELECT name, job, age
FROM friends
WHERE job IS NULL;
```

```
직업이 입력되지 않은 친구 추출.
```



```
SELECT name, job, age, height
FROM friends
WHERE age = 30 AND height >= 175;
```

```
나이가 30살이면서 키가 175이상인 친구들 추출
```



```
SELECT name, job, age, height
FROM friends
WHERE job = 'developer' AND NOT age = 30 AND NOT height BETWEEN 170 AND 180;
```

```
직업이 개발자이면서, 나이가 30살이 아니면서, 키가 170이상 180이하가 아닌 친구 추출.
```

<hr>

<h1>
  함수
</h1>

내장함수는 단일행함수와 다중행함수로 나눌 수 있습니다.

다중행 함수는 다시 집계함수, 그룹함수, 윈도우함수로 나눌 수 있습니다.

<h3>
  단일행함수
</h3>

1.문자열함수

```
LOWER('HI SQL'); => 'hi sql' : 모든 문자를 소문자로.

UPPER('hi sql'); => 'HI SQL' : 모든 문자를 대문자로.

ASCII('A'); => 65 : 문자나 숫자를 아스키코드번호로 바꾼다.

CHAR(65); => 'A' : 아스키코드 번호를 문자나 숫자로 바꾼다.

CONCAT('hi', 'sql') => 'hi sql' : 문자열 연결
// 'hi' || 'sql'과 동일!

SUBSTR('sql expert', 5, 3); => 'exp' : 문자열 자르기
//5번째 문자부터 3개의 문자열 리턴. 3번째 인자가없으면 마지막 문자까지 리턴

LENGTH('sql expert'); => 10 : 문자열의 길이 리턴

LTRIM('xxxYYZZxYZ', 'x'); => 'YYZZxYZ' : 왼쪽부터 다른문자 만날때까지 해당문자열 제거

RTRIM('XXXYYzzXYzz', 'z') => 'XXXYYzzXY' : 오른쪽에서 다른문자 만날때까지 해당문자열 제거

TRIM('x' FROM 'xxYYZZxYZxx') => 'YYZZxYZ' : 양쪽에서 다른문자 만날때까지 해당문자열 제거

RTRIM('XXYYZZXYZ       '); => 'XXYYZZXYZ' : 오른쪽에서 공백제거
```



2.숫자형함수

``` 
ABS(-15) => 15 : 절대값 리턴
SIGN(-20) => -1 : 양수인지 음수인지 0인지 구별
SIGN(0) => 0
SIGN(20) => 1
MOD(7, 3) => 1 : 첫번째 인자를 두번째 인자로 나눈 나머지
CEIL(38.123) => 39 : 숫자보다 크거나 같은 최소 정수
FLOOR(38.123) => 38 : 숫자보다 작거나 같은 최대 정수
ROUND(38.5235, 3) => 38.524 : 반올림함수. 두번째 인자 소수점까지.
TRUNC(38.5235, 3) => 38.523 : 버림함수. 두번째 인자 소수점까지
```



<h1>
  GROUP BY
</h1>

여러행들의 그룹이 모여서 단 하나의 결과를 돌려주는 다중행 함수.

group by 절은 행들을 소그룹화합니다.

select절, having절, order by절에 사용할 수 있습니다.

```
SELECT position, ROUND(AVG(height), 2)
FROM player
GROUP BY position;
```

```
포지션별 평균키를 추출합니다.
```



```
SELECT 
	t.university 학교
 	COUNT(*)
FROM teacher t
WHERE experience_hour >= 100
GROUP BY university;
```

```
experience_hour가 100보다 크거나 같은 인원들을 대학별로 그룹지어서 각각의 갯수를 샌 결과.
```



<h1>
  HAVING
</h1>

GROUP BY한 결과에 조건을 붙이고 싶을때, 즉 GROUP BY의 WHERE절과 같다고 볼 수 있습니다.

```
SELECT 
	t.university 학교
 	COUNT(*)
FROM teacher t
WHERE experience_hour >= 100
GROUP BY university
HAVING COUNT(*) > 10;
```

```
GROUP BY의 조건에서 COUNT(*)가 10보다 큰 목록 추출
```



```
한가지 주의해야할 점은, COUNT(*)은 null값을 포함한 행의 수를 출력한다는 점입니다.
```



<h1>
  ORDER BY
</h1>

order by절은 SQL문장으로 조회한 데이터들을 목적에 맞게 특정 칼럼을 기준으로 "정렬"하는데 사용됩니다.

```
SELECT name, job, age
FROM friends
ORDER BY name DESC
;
```

```
이름을 기준으로 DESC(내림차순)으로 정렬합니다.
아무것도 안적으면, default로 ASC(오름차순)
```



<h3>
  SELECT 문장 실행 순서
</h3>

```
5. SELECT
1. FROM
2. WHERE
3. GROUP BY
4. HAVING BY
6. ORDER BY 
```

<hr>

<h2>
  조건문
</h2>

```
SELECT
	CASE 
		WHEN s.name != s.nickname THEN s.name
		ELSE
			CASE
				WHEN s.age = 10 THEN '10살'
				ELSE '11살'
			END
	END AS 이중when문
```





<hr>

<h2>처음 데이터를 뽑을때 겪은 시행착오의.. 의식의 흐름의.. 과정..</h2>



1.원하는 데이터의 목록을 가져옵니다.

```
select name,university,major,year,attendance_status,mobile,area_gu,admin_memo,self_introduction,account_sid from teacher;
```



2.뭔가 구려보입니다. 문법을 왜 대문자로쓰는지 조금 느꼈습니다.

특정 조건으로 데이터를 뽑기위한 방법은 이미 알고있습니다.

```
SELECT name,university,major,year,attendance_status,mobile,area_gu,admin_memo,self_introduction,schedule.`updated_at` FROM teacher LEFT JOIN schedule ON teacher.account_sid = schedule.account_sid WHERE (major="소비자아동학부" OR major="아동학전공" OR major="소비자아동학과" OR major="아동학과" OR major="아동학부" OR major="아동 청소년학과" OR major="아동심리학과" OR major="아동학과(인문사회)" OR major="소비자아동학부(소비자학전공)"  OR major="소비자아동학부(아동가족학전공)" OR major="아동청소년학부" OR major="심리 아동학부" OR major="아동학부 아동학전공" OR major="아동가족 사회복지학부" OR major="아동 보육전공"  OR major="아동보육전공" OR major="아동보육복지전공" OR major="아동미술교육과" OR major="아동미술보육과" OR major="아동보육과" OR major="아동보육복지과" OR major="보육복지과" OR major="아동복지보육과" OR major="보육과" OR major="영유아보육과" OR major="유아보육과" OR major="유아특수보육과" OR major="유아교육학과" OR major="아동보육학과" OR major="영유아보육복지과" OR major="아동미술과" OR major="영유아보육학과" OR major="아동미술보육과" OR major="아동보육복지학과" OR major="유아보육계열" OR major="유아특수보육과" OR major="어린이영어보육과" OR major="아동교육상담학과" OR major="아동보육학과" OR major="보육학과" OR major="영유아보육학과" OR major="영유아보육학전공" OR major="불교아동보육학과" OR major="아동보육교육학부" OR major="유아특수재활과" OR major="장애유아보육과" OR major="장애유아보육학과") AND (year=3 OR year=4);
```



3.읽기 너무 어렵습니다...

조금 바꿔봅니다..

3-1.AS를 활용해보려합니다.

3-2.줄바꿈을 사용합니다.

```
SELECT name,university,major,year,attendance_status,mobile,area_gu,admin_memo,self_introduction,s.`updated_at`
FROM teacher AS t
LEFT JOIN schedule AS s
   ON t.account_sid = s.account_sid
WHERE (major="소비자아동학부" OR major="아동학전공" OR major="소비자아동학과" OR major="아동학과" OR major="아동학부" OR major="아동 청소년학과" OR major="아동심리학과" OR major="아동학과(인문사회)" OR major="소비자아동학부(소비자학전공)"  OR major="소비자아동학부(아동가족학전공)" OR major="아동청소년학부" OR major="심리 아동학부" OR major="아동학부 아동학전공" OR major="아동가족 사회복지학부" OR major="아동 보육전공"  OR major="아동보육전공" OR major="아동보육복지전공" OR major="아동미술교육과" OR major="아동미술보육과" OR major="아동보육과" OR major="아동보육복지과" OR major="보육복지과" OR major="아동복지보육과" OR major="보육과" OR major="영유아보육과" OR major="유아보육과" OR major="유아특수보육과" OR major="유아교육학과" OR major="아동보육학과" OR major="영유아보육복지과" OR major="아동미술과" OR major="영유아보육학과" OR major="아동미술보육과" OR major="아동보육복지학과" OR major="유아보육계열" OR major="유아특수보육과" OR major="어린이영어보육과" OR major="아동교육상담학과" OR major="아동보육학과" OR major="보육학과" OR major="영유아보육학과" OR major="영유아보육학전공" OR major="불교아동보육학과" OR major="아동보육교육학부" OR major="유아특수재활과" OR major="장애유아보육과" OR major="장애유아보육학과") AND (t.year=3 OR t.year=4 OR t.attendance_status=3);
```



4.IN을 사용해서 코드를 많이 줄여봅니다!!

```
SELECT name,university,major,year,attendance_status,mobile,area_gu,admin_memo,self_introduction,s.`updated_at`
FROM teacher AS t
LEFT JOIN schedule AS s
   ON t.account_sid = s.account_sid
WHERE major IN("소비자아동학부","아동학전공","소비자아동학과","아동학과","아동학부","아동 청소년학과","아동학과(인문사회)","아동심리학과","소비자아동학부","아동청소년학부","심리 아동학부","아동학부 아동학전공","아동가족 사회복지학부","아동 보육전공","아동보육전공","아동보육복지전공","아동미술교육과","아동미술보육과","아동보육과" ,"아동보육복지과","보육복지과","아동복지보육과","보육과","영유아보육과","유아보육과","유아특수보육과","유아교육학과","아동보육학과","영유아보육복지과","아동미술과","영유아보육학과","아동미술보육과","아동보육복지학과","유아보육계열","유아특수보육과","어린이영어보육과" ,"아동교육상담학과","아동보육학과","보육학과","영유아보육학과","영유아보육학전공","불교아동보육학과","아동보육교육학부","유아특수재활과","장애유아보육과","장애유아보육학과") AND (t.year=3 OR t.year=4 OR t.attendance_status=3);
```

훨씬 짧아졌군요..



5.

너무 긴 string데이터를 2단어만 보여주도록 바꿉니다.

게다가 IN을 써도 저건 뭔가 너무 많습니다...

5-1.SUBSTRING_INDEX를 사용

5-2.LIKE를 사용

```
SELECT name,university,major,year,attendance_status,mobile,SUBSTRING_INDEX(address,' ', 2),admin_memo,self_introduction,s.`updated_at`
FROM teacher AS t
LEFT JOIN schedule AS s
   ON t.account_sid = s.account_sid
WHERE (major LIKE '%아동%' OR major LIKE '%보육%' OR major LIKE '%유아%') AND (t.year=3 OR t.year=4 OR t.attendance_status=3);
```

단어를 다 나열하기보다는, 중복되는 특정단어를 포함한 데이터를 불러오는 식으로 수정했습니다.

코드도 훨씬 짧아지고, 검색되는 데이터의 양도 폭발적으로 늘어났습니다...!!



6.왜 선조들은 인덴팅을 만들었는가..를 느낍니다.

6-1. 인덴팅 추가

6-2 AS로 title column수정

6-3.WHEN THEN구문을 사용해서 데이터를 읽을 사람에게 편의제공.

```
SELECT 
	name AS 이름,
	university AS 학교,
	major AS 학과,
	year AS 학년,
	CASE
		WHEN t.attendance_status = 1 THEN '재학'
		WHEN t.attendance_status = 2 THEN '휴학'
		WHEN t.attendance_status = 3 THEN '졸업'
	END AS 졸업여부,
	mobile AS 휴대폰,
	SUBSTRING_INDEX(address,' ', 2) AS 주소,
	admin_memo AS 관리자메모,
	self_introduction AS 자기소개,
	s.`updated_at` AS 최근스케쥴업데이트
FROM teacher AS t
LEFT JOIN schedule AS s
   ON t.account_sid = s.account_sid
WHERE 
	(major LIKE '%아동%' OR major LIKE '%보육%' OR major LIKE '%유아%') 
	AND 
	(t.year=3 OR t.year=4 OR t.attendance_status=3);
```



훨씬 좋아진듯합니다..



<hr>

<h1>
  서브쿼리
</h1>

서브쿼리란 하나의 sql문 안에 포함되어있는 또 다른 sql문입니다.

서브쿼리를 사용하는 이유는, 아렬지지않은 기준을 이용한 검색을 하기위해서라고 합니다.

서브커리는 메인쿼리의 컬럼을 모두 사용할 수 있지만, 메인쿼리는 서브쿼리의 컬럼을 사용 못한다고 합니다.

<h3>
  서브쿼리를 쓸 때 주의사항
</h3>

- 반드시 괄호로 감싸서 사용할 것
- 단일행 또는 복수행 비교연산자 사용가능. 단, 단일행 비교연산자는 서브쿼리의 결과가 반드시 1건 이하.
- 서브쿼리에서 ORDER BY 사용불가. 메인쿼리의 마지막 문장에 위치해야함.



1.단일행 서브쿼리

```
SELECT player_name 선수명, position 포지션, back_no 백넘버
FROM player
WHERE height <= (SELECT AVG(height)
									FROM player)
ORDER BY player_name
;
```

평균키를 알아내는 서브쿼리와, 그 결과로 평균키 이하인 선수를 출력했습니다.



2.다중행 서브쿼리

- 서브쿼리의 결과가 2건이상 반환될 수 있다면, "반드시" 다중행 비교연산자(IN, ALL, ANY, SOME)과 함께 사용해야합니다.

  - IN(서브쿼리) : 서브쿼리의 결과에 존재하는 값과 동일한 조건을 의미
  - 비교연산자 ALL(서브쿼리) : 비교연산자에 ">"를 썼다면, ALL이 모든 값을 만족하는 조건이기 때문에 결과중에 가장 큰값보다 커야 만족한다는 뜻
  - 비교연산자 ANY(서브쿼리) : 비교연산자에 ">"를 썼다면, ANY가 어떤 하나라도 맞는지 확인하는 조건이기 때문에 결과중에 가장 작은값보다 크면 만족한다는 뜻.( = SOME )

  - EXISTS(서브쿼리) : 서브쿼리의 결과를 만족하는 값이 존재하는지 여부 확인. 1건만 찾으면 더이상 검색 안함.

```
SELECT 
	t.name 이름,
	t.university 학교
FROM teacher t
WHERE t.name IN (SELECT t.name FROM teacher t WHERE t.name="누누")
ORDER BY t.name
;
```

누누라는 사람이 두명 이상일 때, 이름과 학교를 출력합니다.

```
내가 이해한 과정
SELECT로 name, university를 출력할 것을 선택합니다.
이 정보는 FROM으로 teacher에서 가져오려합니다.
WHERE로 조건을 선택합니다.
서브쿼리의 SELECT로 name을.. teacher로 부터.. name이 "누누"인 사람들을..IN 연산자를 사용했기에 특정값 여러개를 선택하였습니다..
ORDER BY로 이러한 순서를 이름으로 정렬했습니다.
```



3.다중 컬럼 서브쿼리

- 서브쿼리 결과로 여러 개의 컬럼이 반환되어 메인쿼리 조건과 동시에 비교되는 것.

```
SELECT 
	name 이름,
	university 학교
	experience_hour 누적시간
FROM teacher
WHERE (university, experience_hour) IN (SELECT university, MAX(experience_hour) FROM teacher GROUP BY university)
ORDER BY experience_hour DESC;
```

학교별로 experience_hour가 가장 큰 사람들의 정보를 출력.







