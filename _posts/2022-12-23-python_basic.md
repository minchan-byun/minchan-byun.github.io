---
layout: single
title:  "[멋사] 2일차 Python 베이직"
---

[멋쟁이사자처럼 8기 2일차 교육] list, dictionary, for, while

1일차 교육에 이어 핵심 문법 및 개념에 대해 학습하고, 반복문의 개념을 익혔다.


### 친구야 안녕 


```python
import numpy as np
```


```python
food1 = input("내가 먹은 음식의 가격 : ")
food2 = input("친구가 먹은 음식의 가격 : ")

#print(food1 + food2) # 해당 값은 문자열로 나옴. 

food1 = int(food1) # 문자열 -> 숫자형
food2 = int(food2)

print(food1+food2)

```

    내가 먹은 음식의 가격 : 200000
    친구가 먹은 음식의 가격 : 30300
    230300
    


```python
월세 = int(input("월세를 입력해주세요: "))
관리비 = int(input('관리비를 입력하세요: '))

print((월세 + 관리비)*12)
```

    월세를 입력해주세요: 2020
    관리비를 입력하세요: 2020
    48480
    

### 중식당 주문 : list 알아보기 


```python
orders= ['짜장','탕수육','짬뽕'] 
print(orders)
```

    ['짜장', '탕수육', '짬뽕']
    

    list []에 data 추가하기 : .append(), .insert()


```python
orders= ['짜장','탕수육','짬뽕']

# append(추가하는 데이터 값)
orders.append('냉면')
print(orders)

# insert(index순서, 추가하는 데이터 값) 
orders.insert(3, '양장피')
print(orders
```

    ['짜장', '탕수육', '짬뽕', '냉면']
    ['짜장', '탕수육', '짬뽕', '양장피', '냉면']
    

    list []에서 data 삭제하기 : del , .remove()


```python
# del 'list 이름'[순서]
orders= ['짜장','탕수육','짬뽕']
del orders[0]
orders

# .remove('데이터 값')
orders= ['짜장','탕수육','짬뽕']

orders.remove('짜장')
orders

```




    ['탕수육', '짬뽕']



    길이 측정 : len()
    합 : sum()
    평균 : sum() / len() or np.mean()
    최대, 최소 : max() , min() 
    


```python
orders= ['짜장','탕수육','짬뽕']
print(len(orders))

# 숫자로 구성된 list
num = [20,40, 50, 10, 30]

# 리스트의 합을 구하기.
print(num[0] + num[1] + num[2] + num[3] + num[4])

print(sum(num))

# 리스트의 평균
print('평균구하기 1:',sum(num)/len(num))
print('평균구하기 2:',np.mean(num))

# 리스트의 최대 최소값
print('최대값:', max(num))
print('최소값:', min(num))
```

    3
    150
    150
    평균구하기 1: 30.0
    평균구하기 2: 30.0
    최대값: 50
    최소값: 10
    

### 중식당 메뉴판 만들기 : Dictionary


```python
menu = {"짜장" : 4000, "짬뽕" : 5000, "탕수육" : 9000}

# 딕셔너리 추가 
menu['냉면'] = 5000

# value값 출력 
print(menu['짜장'])

# value값 수정 
menu['탕수육'] = 8500
menu

# key 값 삭제 
del menu['냉면']
menu
```

    4000
    




    {'짜장': 4000, '짬뽕': 5000, '탕수육': 8500}



### 학번 계산기 : IF문 
    - 조건 : True or False로 출력되는 조건들. (관계연산자)
      != , == , > , >=


```python
myGrade = int(input("학번을 입력하세요 : "))
yourGrade = 15

print(myGrade != yourGrade) 
```

    학번을 입력하세요 : 17
    True
    


```python
myGrade = int(input("나의 학번을 입력하세요 : "))
yourGrade = int(input("너의 학번을 입력하세요 : "))

if myGrade == yourGrade:           # True 일때 실행
    print('동기네요!')
elif myGrade < yourGrade:
    print('안녕하세요 후배님.')
else:                              # False일때 실행
    print('안녕하세요. 선배님.')
```

    나의 학번을 입력하세요 : 17
    너의 학번을 입력하세요 : 19
    안녕하세요 후배님.
    

### 지금 주문 되나요? with list


```python
orders= ['짜장','탕수육','짬뽕']

food = input('먹고 싶은 메뉴를 입력해주세요:')

if food in orders:
    print('주문 가능합니다.')
else:
    print('주문이 불가능합니다.')
```

    먹고 싶은 메뉴를 입력해주세요:국수
    주문이 불가능합니다.
    

### 지금 주문 되나요? with 딕셔너리


```python
menu = {"짜장" : 4000, "짬뽕" : 5000, "탕수육" : 9000}
food = input('먹고 싶은 메뉴를 입력해주세요:')

if food in menu:
    print('주문 가능')
else:
    print('주문 불가능')
```

    먹고 싶은 메뉴를 입력해주세요:국수
    주문 불가능
    


```python
menu = {"짜장" : 4000, "짬뽕" : 5000, "탕수육" : 9000}
food = input('먹고 싶은 메뉴를 입력해주세요:')

if food in menu:
    print(menu[food], '원입니다.')
else:
    print('주문 불가합니다.')
```

    먹고 싶은 메뉴를 입력해주세요:탕수육
    9000 원입니다.
    

### 무한 반복: while 문 
    while문 : 조건이 True인 동안에는 계속 실행 


```python
i = 5
while i >= 0:
    print('True')
    i= i-1
```

    True
    True
    True
    True
    True
    True
    


```python
# break 문: 반복문을 빠져나가기 
i = 0 
while True:
    print(i)
    i = i +1
    
    if i >=3:
        print('if문 동작')
        break
print('반복문 종료')
```

    0
    1
    2
    if문 동작
    반복문 종료
    


```python
# continue문 : 반복이 게속해서 돌 수 있도록 while의 조건식으로 다시 올라간다. 
i = 0 
while i < 10:
    i = i+1
    
    if i % 2 == 0:
        continue
    print(i)
    
print('반복 종료.')
```

    1
    3
    5
    7
    9
    반복 종료.
    

### for문  
    - for 변수 in 시퀀스:
         실행될 코드 
    여기서 실행될 코드는 시퀀스의 길이만큼 반복한다. 
    시쿼스의 순서대로 반복하다가 마지막에 반복 종료. 


```python
for i in [10,20,30]:
    print('안녕하세요.') 
    # 리스트에 있는 데이터가 3개로 3개의 인덱스를 지나서 안녕하세요. 가 3번 출력하고 끝남.
```

    안녕하세요.
    안녕하세요.
    안녕하세요.
    


```python
# range(시작숫자, 종료숫자, 스텝)    

# 종료숫자가 3 : 0~3까지 반복 
for i in range(3): 
    print('안녕하세요.')

# 시작숫자=1, 종료숫자=3 : 1부터 3까지만 증가하면서 반복 
for i in range(1,3): 
    print('반가워요.')
```

    안녕하세요.
    안녕하세요.
    안녕하세요.
    반가워요.
    반가워요.
    


```python
# 3부터 시작, 30까지, 3씨 건너서
for i in range(3,31,3): 
    print(i)
```

    3
    6
    9
    12
    15
    18
    21
    24
    27
    30
    


```python
result=0
for i in range(1,101):
    result = result + i 
print(result)
```

    5050
    
