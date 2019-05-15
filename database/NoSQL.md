<h1>
  NoSQL
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

    