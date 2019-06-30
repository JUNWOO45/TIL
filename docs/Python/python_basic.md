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



### string.split()

```
test_str = "web-js-python"
test_str.split('-')	//['web', 'js', 'python']

test2_str = "web js py"
test2_str.split(' ')	//['web', 'js', 'py']

test3_str = "bcabadefaghi"

print(test3_str.split('a'))
```

기본적으로 메서드 사용방법은 js와 동일한듯합니다!



### docstring

```
#이거슨 주석입니다.
'''이것도 주석입니다'''
```



### escape code

```
\n : 줄바꿈
\t : tab
```

```
print('junwoo')	
//'junwoo'

print('jun\nwoo')	
//jun
//woo

print('jun\twoo')
//jun	   woo
```



## list



### append

```
my_list = []
my_list.append('red')
my_list.append('blue')
print(my_list)	//['red', 'blue']
```

js array의 push구나.

### del

```
del ani[2]

ani	//['다람쥐', '사자']
```

### slicing

```
my_list = ['a', 'b', 'c', 'd', 'e']
my_list[0:3]	//['a', 'b', 'c']
my_list[2:]	//['c', 'd', 'e']
my_list[:1]	//['a']
```

### list.sort()

```
test_list=['go', 'mama', 'abe', 'abc', 'def','ccc']
test_list.sort()
test_list	// ['abc', 'abe', 'ccc', 'def', 'go', 'mama']
```

이런식으로 메서드 사용하는구먼….



## Tuple

list와 비슷하지만 값을 변경할 수 없다!

```
my_tuple = (1, 2, 3)
my_tuple	//(1, 2, 3)
```

괄호 없어도 tuple임.

```
my_tuple = 1, 2, 3
my_tuple	//(1, 2, 3)
```

### Packing과 Unpacking

```
my_tuple = 1, 2, 3
```

이게 packing. 

1,2,3을 my_tuple로 포장한다고 생각.

```
num1, num2, num3 = my_tuple

num1	//1
num2	//2
num3	//3
```

이게 unpacking



## for

```python
test_list=['go', 'mama', 'abe', 'abc', 'def','ccc']
for item in test_list:
  print(item)
  'go'
  'mama'
  'abe'
  'abc'
  'def'
  'ccc'
```



### range()

```python
for n in [0, 1, 2]:
  print(n)

//0, 1, 2
```

이거와 다음건 같다!

```python
for n in range(0, 3):
  print(n)
  
//0, 1, 2
```

```
for n in range(2, 6):
	print(n)

//2, 3, 4, 5
```

음.. 다음과 같을때 엄청 편하겠구나!

```python
for n in [1, 2, 3, 4, ..... 100]:
	print(n)
```

이렇게 하지말고,

```python
for n in range(1, 101):
	print(n)
```



### 이중 for문

```
for i in range(1, 10):
	print('{}x{}={}'.format(2, i, 2*i))
```

이러면 구구단 2단이 출력.

```python
for i in range(2, 10):
  for j in range(1, 10):
    print('{}x{}={}'.format(i, j, i*j))
```

이러면 구구단 9단까지 출력되는구나.

format이 엄청 유용하네.



### comprehension

```
numbers=[1,2,3,4,5,6,7,8,9]
odd_numbers=[]
for number in numbers:
	if number % 2 == 1:
		odd_numbers.append(number)

print(odd_numbers);	//[1,3,5,7,9]
```

이런 식의 코드를 짤 수 있는데, 컴프리헨션을 사용하면

```
[number for number in numbers if number % 2 == 1]
```

이렇게 읽으면 되겠네요.

1.number를 넣을 거다..!

2.numbers를 for문 돌려서, number를 2로 나눈 나머지가 1인 number를 넣을거다!



## Operator (연산자)

### 할당

```
=
+=
-=
*=
/=
```

js와 똑같구나.

### 산술연산자

```
+, -, *, / 는 뻔하고..
** : 제곱
// : 몫
% : 나머지
```

```
3 ** 2	//9
14 // 5	//2
14 % 5	//4
```

### 문자열 연산자

```
+
*
```

문자열 연산자에 *도 있구나.

문자열 연산자 *는 string 과 number의 조합으로 이루어지게됨.ㅇㅇ

```
print('hi' * 2)	// 'hihi'
```



### 비교연산자

```
==, !=
>, >=
<, <=
```

### 논리연산자

```
and
or
not
```

### Membership 연산자

```
in
not in
```

```
name = ['junwoo', 'gaon', 'yeoul']
'junwoo' in name	//True
'hello'	not in name 	//True
```

### if

```
if 조건:
    실행할 명령1
    실행할 명령2
elif 조건:
		실행할 명령3
		실행할 명령4
else:
		실행할 명령5
```

```
name='junwoo'
if name='junwoo':
	print('hello')	//'hello'
```

### while

```
while 조건:
		실행할 명령1
		실행할 명령2
```

```
count=0
while count < 5:
		print('count is : ', count)
		count += 1
 

count is :  0
count is :  1
count is :  2
count is :  3
count is :  4
```

### continue, break

```
while count < 10:
		count += 1
		if count < 4:
				continue
		print('count : ', count)
		if count == 8
			break
			
count :  4
count :  5
count :  6
count :  7
count :  8
```

continue는 만나면 아랫줄은 실행하지않고 다시 while문 처음으로 돌아가버리네.

break는 조건 만족하면 while문을 끝내버리고.



##Dictionary

자바스크립트의 object네요.

```
my_dict = {}
my_dict['name'] = 'junwoo'
my_dict['age'] = 100

print(my_dict)		//{'name': 'junwoo', 'age': 100}

del my_dict['age']

print(my_dict)		//{'name': 'junwoo'}
```

### method

메소드는 검색해서 알아내면 되니깐… 라고 변명하며 넘어간다..!

기본적인 메소드 하나 사용해보면.

```
my_dict={'name':'junwoo','age':10,'live':'dongtang'}

for value in my_dict.values():
		print(value)
		
		
junwoo
10
dongtan

for keylist in my_dict.keys():
	print(keylist)
	

name
age
live

for item in my_dict.items():
	print(item)


('name', 'junwoo')
('age', 10)
('live', 'dongtang')
```