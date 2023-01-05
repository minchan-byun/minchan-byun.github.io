---
layout: single
title:  "[멋사] Python 클래스와 상속"
---

[멋쟁이사자처럼 8기 Python] 클래스 정의 및 생성, 클래스 메소드 작성, 상속, 데코레이터  

[summary : function]
- 반복되는 코드를 묶어서 사용 > 코드의 유지보수 향상
- 사용법 : 함수선언(코드작성) > 함수호출(코드실행)  

1. **def, return, argument, parameter, docstring, scope, global, lambda**
2. **argument, parameter** : 함수호출하는 코드에서 함수선언하는 코드로 데이터를 전달
3. **default parameter, keyword argument**
    - *args, **kwargs
        - **parameter** : 여러개 아규먼트 > 하나의 변수(tuple,dict)로 묶어서 코드실행
        - **argument** : 하나의 변수(list,tuple,dict) > 여러개 아규먼트로 풀어서 코드실행(함수호출)
4. **return** : 함수를 실행한 결과를 변수에 저장 : 함수의 코드실행 중단
5. **docstring** : 함수의 설명글 작성 : 함수를 선언하는 코드 바로 아래에 멀티라인 문자열로 작성 : help()
6. **scope** : 함수안에서 선언(지역:local) : 함수밖에서 선언(전역:global)
  - 지역영역에서 전역영역의 변수를 가져올때 : **global**
  - 전역영역에서 지역영역의 변수를 가져올때 : **return**
7. **lambda** : 일회성 함수 : 간단한 함수(파라미터,리턴)를 함수 선언없이 함수의 기능을 사용가능

- 함수: 클래스 밖에서 선언된 함수
- 메소드: 클래스 안에서 선언된 함수

[class]  
변수, 함수를 묶어서 코드를 작성하는 방법
객체지향 구현하는 문법
  - 객체지향 : 실제세계를 모델링하여 프로그램을 개발하는 개발 방법론 : 협업을 용이하게 하기 위한
함수 사용법 : 함수선언(코드작성) > 함수호출(코드실행)
클래스 사용법
  - 클래스선언(코드작성) > 객체생성(메모리사용) > 메서드실행(코드실행)
  - 클래스선언(설계도작성) > 객체생성(제품생산) > 메서드실행(기능사용)
식별자 컨벤션
  - 변수, 함수 : snake_case
  - 클래스 : PascalCase, UpperCamelCase
class, self, 사용자 정의 데이터 타입, spacial methods(__init__(), __add__() ...)
상속, super, getter-setter, mangling, 메서드의 종류들(인스턴스,클래스,스태틱) 

#### 1. 클래스선언 : 코드작성
- 계산기 설계 : Calculator : number1, number2, plus(), minus()


```python
class Calculator:

    number1, number2 = 1, 2 # 변수 초기값 설정

    def plus(self):
        return self.number1 + self.number2
    
    def minus(self):
        return self.number1 - self.number2
```

#### 2. 객체생성 : 메모리사용
이 객체 생성 과정은 제조업으로 보았을 때 설계된 제품을 생성하는 과정이다. 
제조업에서는 이 과정에서 상당한 비용이 많이 들지만, 소프트웨어 산업에서는 매우 간단하다.


```python
calc1 = Calculator() # 파스칼 케이스 == 클래스를 객체로 만들어준다.
calc2 = Calculator()

# dir() : 객체에 들어있는 변수를 출력
[var for var in dir(calc1) if var[0] != '_']
```




    ['minus', 'number1', 'number2', 'plus']




```python
calc1.number1, calc1.number2
```




    (1, 2)



#### 3. 메서드 실행 : 코드 실행


```python
calc1.plus(), calc1.minus()
```




    (3, -1)




```python
# 클래스선언 : 은행계좌 : Account : balance, insert(), withdraw()
class Account:
    
    balance = 0

    def insert(self, amount):
        balance += amount
    
    def withdraw(self, amount):
        if balance >= amount:
            balance -= amount
        else:
            print(f'잔액이 {amount - balance}원 부족합니다.')
```


```python
# 객체생성
account_1 = Account()
account_2 = Account()
account_1.balance, account_2.balance
```




    (0, 0)




```python
# 메서드실행
account_1.insert(10000)
account_1.balance, account_2.balance
```

- 스페셜 메서드 특별한 기능을 하는 메서드 : 앞뒤로 __를 붙임  

- 생성자 메서드 : __init__()   
    객체를 생성할때 실행되는 메서드  
    변수의 초기값을 설정할때 주로 사용  
    불량 객체(메서드 사용 X)가 만들어질 확률을 줄여줌


```python
# 클래스 생성
class Account:
    def insert(self, amount):
        self.balance += amount
    
    def withdraw(self, amount):
        if self.balance >= amount:
            self.balance -= amount
        else:
            print(f'잔액이 {amount - self.balance}원 부족합니다.')
```


```python
# 클래스생성 : 설계도작성
class Account:
    def __init__(self, balance):
        self.balance = balance

    def insert(self, amount):
        self.balance += amount
    
    def withdraw(self, amount):
        if self.balance >= amount:
            self.balance -= amount
        else:
            print(f'잔액이 {amount - self.balance}원 부족합니다.')
```

* account의 데이터 타입은 Account
* account 객체가 만들어진 클래스는 Account
* 데이터 타입 == 클래스 > 클래스는 데이터 타입이다.
* Account 클래스는 우리가 만듦 > 사용자 정의  
  -> 클래스는 사용자 정의 데이터 타입이다.


```python
# 객체의 데이터 타입에 따라서 사용할수 있는 변수, 메서드가 다르다.
data1, data2 = 'python', [1, 2, 3]
print(type(data1), type(data2))
print([var for var in dir(data1) if var[0] != '_'])
print([var for var in dir(data2) if var[0] != '_'])
```

d1 + d2 : d1.__add__(d2) : d1.__add__() : int 클래스의 __add__() 메서드  
d3 + d4 : d3.__add__(d4) : d3.__add__() : str 클래스의 __add__() 메서드  
> 데이터 타입에 따라서 수행되는  __add__() 메서드가 다르다.


```python
# 덧셈연산을 하지만 뺄셈연산이 수행되는 객체를 생성
class Number:

    def __init__(self, data):
        self.data = data
    
    def __add__(self, obj):
        return self.data - obj.data

    def __str__(self):
        return str(self.data)

    def __repr__(self):
        return str(self.data)
```

#### 상속
다른 클래스의 변수(메서드)를 가져와서 사용하는 방법

iPhone1 : call  
iPhone2 : call, send_msg  
iPhone3 : call, send_msg, internet


```python
class iPhone1:
    def call(self):
        print('calling!')
        
        
class iPhone2:
    def call(self):
        print('calling!')
    def send_msg(self):
        print('send_msg!')
        
        
class iPhone3:
    def call(self):
        print('calling!')
    def send_msg(self):
        print('send_msg!')
    def internet(self):
        print('internet!')
```


```python
iphone1 = iPhone1()
iphone2 = iPhone2()
iphone3 = iPhone3()
```


```python
def show_vars(obj):
    return [var for var in dir(obj) if var[0] != '_']

show_vars(iphone1), show_vars(iphone2), show_vars(iphone3)
```




    (['call'], ['call', 'send_msg'], ['call', 'internet', 'send_msg'])




```python
# 상속 사용
class iPhone1:
    def call(self):
        print('calling!')

class iPhone2(iPhone1):
    def send_msg(self):
        print('send_msg!')

class iPhone3(iPhone2):
    def internet(self):
        print('internet!')
```


```python
# 다중상속
class Human:
    def walk(self):
        print('walking!')

class Korean:
    def eat(self):
        print('eat kimchi!')

class Indian:
    def eat(self):
        print('eat curry!')
```

#### 데코레이터 : decorator
 함수에서 중복되는 코드를 빼서 데코레이터 함수로 만들어 코드를 작성하는 방법
 원래 있던 함수에 새로운 기능을 추가한 함수로 변경할때 주로 사용


```python
def func1():
    print('code1')
    print('code2')
    print('code3')

def func2():
    print('code1')
    print('code4')
    print('code3')
```


```python
def deco(func):
    def wrapper(*args, **kwargs):
        print('code1')
        func()
        print('code3')
    return wrapper
```

 - deco 함수의 파라미터 func에 func1이 들어감
 - func1 함수는 deco 함수의 return 함수인 wrapper 함수로 변경


```python
@deco
def func1():
    print('code2')

@deco
def func2():
    print('code4')

func1()
func2()
```

    code1
    code2
    code3
    code1
    code4
    code3
    


```python
# timer 데코레이터 함수 생성
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time() # 현재시간 저장
        result = func(*args, **kwargs)
        end = time.time() # 현재시간 저장
        print(f'running time : {end - start} sec')
        return result
    return wrapper
```


```python
def plus(n1, n2):
    return n1 + n2

def minus(n1, n2):
    return n1 - n2
```


```python
# 패스워드를 맞춰야 함수의 실행이 가능하도록 하는 데코레이터 작성
def admin(func):
    def wrapper(*args, **kwargs):
        

    return wrapper
```


```python
# 패스워드를 맞춰야 함수의 실행이 가능하도록 하는 데코레이터 작성
def admin(func):
    def wrapper(*args, **kwargs):
        pw = input('insert password : ')
        if pw == 'python': # 패스워드 맞음
            result = func(*args, **kwargs)
        else: # 패스워드 맞지 않음
            result = 'wrong password!'
        return result
    return wrapper
```


```python
def plus(n1, n2):
    return n1 + n2

@admin
def minus(n1, n2):
    return n1 - n2
```


```python
def variance(data):
    var = 0
    x_ = sum(data) / len(data)
    for xi in data:
        var += (xi - x_) ** 2
    return var / len(data)
```


```python
variance(data1), variance(data2), variance(data3)
variance(data1) ** 0.5, variance(data2) ** 0.5, variance(data3) ** 0.5
np.var(data1), np.var(data2), np.var(data3)
```


```python
# - 1 : 자유도
def covariance(x, y):
    cov = 0
    x_ = sum(x) / len(x)
    y_ = sum(y) / len(y)
    for xi, yi in zip(x, y):
        cov += (xi - x_) * (yi - y_)
    return cov / (len(x) - 1)
```


```python
# 공분산의 한계 : 방향성은 보여줄수 있으나, 강도는 보여줄수 없음
data4 = [data * 10 for data in data1]
data5 = [data * 10 for data in data3]
data1, data3, data4, data5
```


```python
def covariance(x, y):
    cov, x_, y_ = 0, sum(x) / len(x), sum(y) / len(y)
    for xi, yi in zip(x, y):
        cov += (xi - x_) * (yi - y_)
    return cov / len(x)
def cc(x, y):
    cov = covariance(x, y)
    var = (variance(x) * variance(y)) ** 0.5
    return cov / var
```


```python
data1, data2, data3, data4, data5
```


```python
# 1과 가까울수로 강한 양의 상관관계
# -1과 가까울수록 강한 음의 상관관계
# 0과 가까울수록 관계없음
cc(data1, data2), cc(data1, data3)
```
