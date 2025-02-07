---
layout: single
title:  "[멋사] Python 함수 개념 및 응용"
---

[멋쟁이사자처럼 8기 Python] function, (*args, **keywars), lamda, list comprehension, map 

오늘은 함수의 개념과 함수에 적용되는 argument, parameter에 대해 자세하게 배웠다.
또한, lamda, list comprehension, map 과 같은 응용되는 함수를 다뤘다. 

지난 수업 summary  
3. 연산자
  - CPU를 사용하는 문법
  - 산술 : +, -, *, /, //, %, ** : 데이터 + 데이터 = 데이터
  - 할당 : 식별자 <산술>= 데이터
  - 비교 : ==, !=, >, <, >=, <= : 데이터 + 데이터 = 논리값 : 조건1개
  - 논리 : not, and(True), or(False) : 논리값 + 논리값 = 논리값 : 조건2개 이상
  - 멤버 : in, not in : 컬렉션 데이터에 특정 데이터가 있는지 확인 : 결과 논리값
  
4. 조건문
  - 특정 조건에 따라서 다른 코드를 실행하는 문법
  - if, elif, else
  - 조건을 확인하는 코드에서 데이터가 논리값(bool)이 아니면 bool() 형변환해서 확인
  
5. 반복문
  - 특정 코드를 반복적으로 실행하는 문법
  - while, for, break, continue, range(), enumerate(), zip()
  

복습 Quiz. 로또 번호 출력 (list)
- 1 ~ 45의 랜덤한 숫자 6개 출력 
- 숫자 6개가 중복 x


```python
# 선생님 풀이
import random

# 1. 로또번호 저장 변수 생성
lotto = []

# 2. 아래의 코드 반복 : while
while True:

#   2-1. 1 ~ 45 랜덤한 숫자 출력 후 저장 : random_number : random.randint()
    random_number = random.randint(1, 45)

#   2-2. lotto 리스트에 random_number 없으면, random_number를 lotto 변수에 추가 : list.append()
    # if random_number not in lotto:
    #     lotto.append(random_number)

#   2-2. random_number를 lotto 변수에 추가 : list.append()
    lotto.append(random_number)
    lotto = list(set(lotto))

#   2-3. lotto의 데이터 갯수가 6개 이상이면 반복 중단 : if, len(), break
    if len(lotto) >= 6:
        break

# 3. 로또번호 출력 : print()
lotto.sort()
print(lotto)
```

    [11, 13, 20, 22, 31, 36]
    


```python
# 내 풀이
import random

a = []    
for i in range(1,46):
    a.append(i)

lotto = random.sample(a, 6)
print(lotto)
```

    [5, 38, 27, 15, 24, 9]
    

### 함수 
    함수란? 반복적으로 사용되는 코드를 묶어서 사용하는 방법 > 코드의 유지보수가 쉬워짐 
    함수를 선언할 때 코드를 작성하고, 함수를 호출할 때 코드를 실행한다. 
    
- def, return, argument, parameter, docstring, scope, lambda
- 사용법 : 함수선언(코드작성) > 함수호출(코드실행)


```python
# 함수선언(코드작성)
def plus(n1, n2): # n1, n2 : parameter
    print(n1 + n2)

# 함수호출(코드실행)
plus(1, 2) # 1, 2 : argument
```

    3
    

- parameter와 argment의 개수가 맞아야 에러가 안난다. 
- parameter에 default 값을 넣어주면 argment를 쓰지 않아도 에러 없이 실행이 가능하다.  
- keyword argment


```python
# 함수선언(코드작성)
def plus(n1, n2=10, n3=20): # n1 : parameter, n2=10, n3=20 : default parameter
    print(n1 + n2 + n3)

# 함수호출(코드실행)
plus(1, n3=100) # 1 : argument, n3=1000 : keyword argumnet
```

    111
    


```python
import random

# 함수선언
def display_lotto(count): # count : parameter
    lotto = []
    while True:
        random_number = random.randint(1, 45)
        lotto.append(random_number)
        lotto = list(set(lotto))
        if len(lotto) >= count:
            break
    lotto.sort()
    print(lotto)

# 로또번호출력 : 6개
display_lotto(6) # 6 : argument

# 로또번호출력 : 7개
display_lotto(7)
```

    [5, 7, 13, 15, 19, 23]
    [12, 14, 26, 31, 33, 35, 36]
    


```python
# 내 풀이 함수 선언
import random

def lotto(count):  # count : parameter
    lotto_number = []    
    for i in range(1,46):
        lotto_number.append(i)

    lotto = random.sample(lotto_number, count)  # count : argument
    print(lotto)
    
lotto(6)
```

    [34, 45, 19, 37, 42, 23]
    

Quiz. 
lotto()를 호출할 때 파라미더가 없으면 1~45까지 6개의 숫자를 출력하고, 
숫자의 범위와 숫자의 개수를 argment로 설정해 함수를 호출할 수 있도록 함수를 작성하시오. 




```python
import random

def lotto(end=46,count=6):  
    lotto_number = []    
    for i in range(1,46):
        lotto_number.append(i)

    lotto = random.sample(lotto_number, count)  
    print(lotto)
    
lotto()
```

    [6, 1, 12, 15, 29, 39]
    

#### return  
    - 용도 1. 함수 호출해서 결과 데이터 변수에 저장할 때
    - 용도 2. 함수의 코드 중단할 때


```python
def plus1(n1,n2):
    print(n1+n2)
    
def plus2(n1,n2):
    return n1 + n2

result1 = plus1(1,2)
result2 = plus2(1,2)
print(result1,result2) 
# plus1 함수는 return이 없어 result1에 값이 할달 되지 않아 값이 None임.
```

    3
    None 3
    


```python
# return이 있는 함수 예시 : str.upper()
data = 'python'
result = data.upper()
print(data,result)
```

    python PYTHON
    


```python
# return이 없는 함수 예시 : list.sort()
data=[1,3,2]
result = data.sort()
print(data, result)
```

    [1, 2, 3] None
    


```python
# 함수의 코드 실행 중당

def echo(msg,count=3):
    for i in range(count): # [0,1,2,3,4,5,6]
        if i >= 5:
            return # 함수 코드 중단
        print(msg)
    print('Done')
    
echo('변민찬',7)
```

    변민찬
    변민찬
    변민찬
    변민찬
    변민찬
    


```python
# 여러 데이터를 리턴 by other language
def calc(n1, n2):
    result = [n1 + n2, n1 - n2]
    return result

result = calc(3, 1)
plus = result[0]
minus = result[1]
plus, minus
```




    (4, 2)




```python
# 여러개의 데이터를 리턴 by python 
def calc(n1, n2):
    return n1 + n2, n1 - n2

plus, minus = calc(3, 1)
plus, minus

plus, _ = calc(3, 1) # 필요없는 변수는 '_'로 생략 가능
plus
```




    4



#### docstring : 
    함수의 설명을 작성하는 것   
    함수선언코드 바로 아래에 멀티라인 문자열로 작성
- help() 함수로 docstring 출력 
- docstring에 들어가는 내용
    1. 함수의 설명 
    2. parameter의 설명 
    3. return의 결과 


```python
def plus(n1, n2):
    '''
    1. This function is to plus two numbers.

    2. parameters
    --------
    n1 : int, float : first number
    n2 : int, float : second number

    3. return
    --------
    n1 + n2 : int, float
    '''
    return n1 + n2
```


```python
help(plus)
```

    Help on function plus in module __main__:
    
    plus(n1, n2)
        1. This function is to plus two numbers.
        
        2. parameters
        --------
        n1 : int, float : first number
        n2 : int, float : second number
        
        3. return
        --------
        n1 + n2 : int, float
    
    

#### argment : 개수에 상관없이 함수를 실행하는 방법  
       *args : 여러개의 아규먼트를 튜플 데이터타입으로 받아줌  
       **kwargs : 여러개의 키워드 아규먼트를 딕셔너리 데이터타입으로 받아줌
    


```python
def plus(*args, **kwargs): # 파라미터에 컬렉션 데이터 타입을 받아줌 : 식별자1개, 데이터n개
    print(type(args), args)
    print(type(kwargs), kwargs)
    # return n1 + n2

# 키워드 아규먼트는 키워드가 없는 아규먼트 뒤에 사용
# 디폴트 파라미터는 디폴트 값이 없는 파라미터 뒤에 사용
plus(1, 2, 3, 4, 5, n1=10, n2=30) # 여러개의 아규먼트
```

    <class 'tuple'> (1, 2, 3, 4, 5)
    <class 'dict'> {'n1': 10, 'n2': 30}
    

#####  args, kwargs : argment에서 사용
   - 파라미터 사용 : 여러개의 argment -> 컬렉션 데이터타입(tuple,dict)으로 묶어줌
   - 아규먼트 사용 : 컬렉션 데이터타입(list,tuple,dict) > 여러개의 argment로 풀어줌
   - *args : list, tuple 데이터타입의 데이터를 여러개의 kwargs가 없는 argment로 풀어줌
   - **kwargs : dict 데이터타입의 데이터를 여러개의 kwargs가 있는 argment로 풀어줌


```python
def echo(*args, **kwargs):
    print(type(args), args)
    print(type(kwargs), kwargs)
    
data=[1,2,3]
echo(data)
echo(*data)
```

    <class 'tuple'> ([1, 2, 3],)
    <class 'dict'> {}
    <class 'tuple'> (1, 2, 3)
    <class 'dict'> {}
    

#### scope : 범위
    1. 함수 밖 : 전역영역(global)
    2. 함수 안 : 지역영역(local)


```python
# 실수 할만한 코드 3
data = 10 # global 영역에서의 data
 
def change():
    data = 20 # local 영역에서의 data
    print('local:',data)

change()
print('global:',data)
```

    local: 20
    global: 10
    

##### global : 지역영역에서 전역영역으로의 변수 사용


```python
data = 10

def change():
    global data # global 영역 data 호출  
    print(data)

change()
print(data)
```

    10
    10
    

##### return : 전역영역에서 지역영역의 변수 사용하는 방법


```python
data = 10

def change():
    data = 20  
    return data

data = change()
print(data)
```

    20
    

#### lamda 함수  
    1회성 함수로 간단한 함수(파라미터, 리턴 구성)를 함수 선언 없이 사용 가능  
    -> 메모리 절약, 가독성 증대 
    


```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    


```python
def plus(n1,n2):
    return n1+n2
%whos
```

    Variable   Type        Data/Info
    --------------------------------
    plus       function    <function plus at 0x000001F6E0176160>
    

    함수는 데이터 타입이 function인 변수이다.
    function은 코드를 담고 있는 데이터타입이다.


```python
type(plus)
```




    function




```python
# 함수도 변수이기 때문에 args 로 사용 가능 
# 변수 3개 선언 : plus, minus, calc : 저장공간 3칸 사용함.
def plus(n1,n2):
    return n1+n2

def minus(n1,n2):
    return n1-n2

def calc(func, n1, n2):
    return func(n1,n2)


calc(plus, 1, 2), calc(minus, 1, 2)
# 함수 안에서 다른 함수를 사용해야하는 경우에 활용
```




    (3, -1)




```python
# 저장공간 1칸만 사용해서 구현한다면? lamda 함수 활용 
# lambda 함수 : 간단한 함수를 함수 선언 없이 사용 가능
func = lambda n1, n2: n1 + n2
func(1, 2)
```


```python
calc(lambda n1, n2: n1 + n2, 1, 2), calc(lambda n1, n2: n1 - n2, 1, 2)
```




    (3, -1)



#### list comprehension : 리스트 컴프리헨션
    간단한 반복문, 조건문을 사용해서 리스트 데이터를 만들때 사용하는 문법
    주로 리스트 데이터를 필터링 하거나 데이터를 변경할때 사용


```python
# 0 ~ 9 까지의 데이터에서 홀수만 뽑아서 제곱한 결과를 리스트로 출력
result = []
for number in range(10):
    if number % 2:
        result.append(number ** 2)
result
```




    [1, 9, 25, 49, 81]




```python
reports = ['사업보고서(2020)', '감사보고서(2021)', '[기재정정]사업보고서(2020)']
# 2020년도 보고서 목록을 리스트로 출력
reports_2020 = [report[:-6] for report in reports if report[-5:-1] == '2020']
reports_2020
```




    ['사업보고서', '[기재정정]사업보고서']




```python
reports_2020 = {report[:-6]: report[-5:-1] for report in reports if report[-5:-1] == '2020'}
reports_2020
```




    {'사업보고서': '2020', '[기재정정]사업보고서': '2020'}




```python
# kim씨 성을 가진 이름을 연령대로 데이터를 바꿔서 리스트로 출력
names = ['kim python(23)', 'lee notebook(32)', 'kim macbook(47)']
def ages(data):
    return data[:-3] + str(int(data[-3:-1]) // 10 * 10) + ')'

names_kim = [
    ages(name)
    for name in names 
    if name.split(' ')[0] == 'kim'
]

names_kim
```




    ['kim python(20)', 'kim macbook(40)']



#### map()
    iterable한 데이터의 모든 value에 특정 함수를 적용한 결과를 리스트로 출력


```python
names = ['kim python(23)', 'lee notebook(32)', 'kim macbook(47)']

def ages(data):
    return data[:-3] + str(int(data[-3:-1]) // 10 * 10) + ')'
```


```python
names = ['kim python(23)', 'lee notebook(32)', 'kim macbook(47)']

def ages(data):
    return data[:-3] + str(int(data[-3:-1]) // 10 * 10) + ')'

list(map(ages, names))
```




    ['kim python(20)', 'lee notebook(30)', 'kim macbook(40)']


