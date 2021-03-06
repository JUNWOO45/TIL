<h1>
  공부한 SQL을 예시와 함께 복습
</h1>



<h2>
  SQL문의 처리 순서
</h2>

```
SELECT phone
FROM customer
WHERE name='김연아'
;
```

1.FROM customer

2.WHERE name='김연아'

3.SELECT phone



<h2>
  SELECT/FROM
</h2>

<hr>

<h3>
  모든 책의 이름과 가격을 검색
</h3>

```
SELECT bookname, price
FROM book
;
```

<h3>
  모든 책의 가격와 이름을 검색
</h3>

```
SELECT price, bookname
FROM book
;
```

<h3>
  모든 책의 번호, 이름, 출판사, 가격을 보여라.
</h3>

```
SELECT bookid, bookname, publisher, price
FROM book
;
```

```
SELECT *
from book
;
```

<h3>
  출판사를 모두 보여라.
</h3>

```
SELECT publisher
FROM book
;
```

<h3>
  출판사를 모두 보여라. 단, 중복은 제거하라.
</h3>

```
SELECT DISTINCT publisher
FROM book
;
```



<h2>
  WHERE
</h2>

<hr>

<h3>
  가격이 20000원 미만인 책을 보여라.
</h3>

```
SELECT *
FROM book
WHERE price < 20000
;
```

<h3>
  이름이 '축구의 역사'인 책의 이름과 출판사를 보여라.
</h3>

```
SELECT bookname, publisher
FROM book
WHERE bookname LIKE '축구의 역사'
;
```

<h3>
  '축구'가 포함된 책 제목, 출판사를 보여라.
</h3>

```
SELECT bookname, publisher
FROM book
WHERE bookname LIKE '%축구%'
;
```

<h3>
  오른쪽 2번째 위치에 '공'이라는 문자를 가지는 출판사를 보여라.
</h3>

```
SELECT *
FROM book
WHERE publisher LIKE '%공_'
;
```



<h2>
  복합 WHERE
</h2>

<hr>

<h3>
  '축구'에 관한 책 중 가격이 20000원 이상인 책을 보여라.
</h3>

```
SELECT *
FROM book
WHERE bookname LIKE '%축구%'
AND price >= 20000
;
```

<h3>
  출판사가 '시공사' 혹은 '대한미디어'인 책을 보여라.
</h3>

```
SELECT *
FROM book
WHERE publisher = '시공사'
OR publisher = '대한미디어'
;
```



<h2>
  IN과 NOT IN
</h2>

<hr>

<h3>
  출판사가 '시공사' 혹은 '대한미디어'인 책을 보여라
</h3>

```
SELECT *
FROM book
WHERE publisher IN ('시공사', '대한미디어')
;
```

<h3>
  출판사가 '시공사'혹은 '대한미디어'가 아닌 책을 보여라
</h3>

```
SELECT *
FROM book
WHERE publisher NOT IN ('시공사', '대한미디어')
;
```



<h2>
  BETWEEN
</h2>

<hr>

<h3>
  가격이 10000원이상, 20000원이하인 책을 보여라
</h3>

```
SELECT *
FROM book
WHERE price BETWEEN 10000 AND 20000
;
```



<h2>
  ORDER BY
</h2>

<hr>

<h3>
  책을 제목 순으로 보여라.
</h3>

```
SELECT *
FROM book
ORDER BY bookname
;
```

<h3>
  책을 가격 순, 제목 순으로 보여라
</h3>

```
SELECT *
FROM book
ORDER BY price, bookname
;
```

<h3>
  책을 가격의 내림차순, 출판사의 오름차순으로 보여라.
</h3>

```
SELECT *
FROM book
ORDER BY price DESC, publisher ASC
;
```



<h2>
  SQL 집계함수
</h2>

<h3>
  고객이 주문한 도서의 총 판매액을 보여라.
</h3>

```
SELECT SUM(saleprice)
FROM orders
;
```

```
SELECT SUM(saleprice) as 총매출
FROM orders
;
```

<h3>
  2번 고객이 주문한 도서의 총 판매액을 보여라.
</h3>

```
SELECT SUM(saleprice) as 총매출
FROM orders
WHERE customer_id = 2
;
```

<h3>
  도서의 총 판매액, 평균값, 최저가, 최고가를 보여라.
</h3>

```
SELECT SUM(saleprice) as 총매출
			 AVG(saleprice) as 평균값
			 MIN(saleprice) as 최저가
			 MAX(saleprice) as 최고가
FROM orders
;
```

<h3>
  판매건수를 보여라
</h3>

```
SELECT COUNT(*)
FROM orders
;
```



<h2>
  GROUP BY
</h2>

<hr>

<h3>
  고객id별로 도서수량과 총액을 구하라
</h3>

```
SELECT customer_id, COUNT(*) AS 도서수량, SUM(saleprice) as 총액
FROM orders
GROUP BY customer_id
;
```

<h3>
  10000원 초과 도서판매를 고객별로 도서수량을 구하여라.
</h3>

```
SELECT customer_id, COUNT(*) AS 도서수량
FROM orders
WHERE saleprice > 10000
GROUP BY customer_id
ORDER BY customer_id
;
```



<h2>
  HAVING
</h2>

<hr>

<h3>
  10000원 초과 도서 판매를 고객별로 도서수량을 구하여라.
  단, 2권 이상 구매한 고객만 구하라.
</h3>

```
SELECT customer_id, COUNT(*) AS 도서수량
FROM orders
WHERE saleprice > 10000
GROUP BY customer_id
HAVING COUNT(*) >= 2
ORDER BY customer_id
;
```





<hr>

공부 자료 출처 : [http://contents.kocw.or.kr/document/lec/2011_2/dunksung/ParkUchang/03.pdf](http://contents.kocw.or.kr/document/lec/2011_2/dunksung/ParkUchang/03.pdf)



