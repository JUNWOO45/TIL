# 파이썬 기초 공부



## 파이썬 자료형

```
숫자형
문자형
불린
리스트 : 자바스크립트 array
튜플 : list와 비슷한데, 값을 바꿀 수 없음.
딕셔너리 : 자바스크립트 object
```



## 자료형 변환

```
my_int = 10
type(my_int)	// <class 'int'>

float(my_int)
1.0
type(float(my_int))	//<class 'float'>

str(my_int)	//'1'
type(str(my_int))	//<class 'str'>
```

```
name = 'junwoo'
list(name)
['j', 'u', 'n', 'w', 'o', 'o']
```



## 주석

```
print('hi') #안녕?
```



## 문자열

- 큰따옴표, 작은따옴표 상관 없음.
- 여러 줄을 저장하는 것도 가능

```
my_str = '''준우
가온
여울'''

// '준우\n가온\n여울'
```



### Formatting

```
my_str = "My name is %s" % 'junwoo'

print(my_str)	//'My name is junwoo'
```

```
'number is %d %d %d' % (10, 20, 30)
'number is 10 20 30'

//%d는 정수형 숫자만 입력 가능.
```

```
'number is %f' % (1.5)
'number is 1.5

//%f는 실수.
```



### format()

```
'my name is %s' % '준우'
'my name is 준우'

'my name is {}'.format('준우')
'my name is 준우'
```

이런식으로 순서대로 들어감.

```
'{} * {} = {}'.format(5, 4, 20)
'5 * 4 = 20'
```

순서를 이렇게 바꿀 수도 있음.. 오오..!

```
'{2} * {0} = {1}'.format(3, 6, 2)
'2 * 3 = 6'
```



### Indexing

```
my_str = '파이썬공부'
my_str[0] = '파'
my_str[-1] = '부'
```



### Slicing

```
my_str = "파이썬공부"
my_str[0:1]	//'파'
my_str[1:3]	//'이썬'

my_str[:3]	//'파이썬'
//앞의 숫자가 없으면 뒷 숫자 전까지.
my_str[3:]	//'공부'
//뒤의 숫자가 없으면 앞숫자부터 끝까지
```

