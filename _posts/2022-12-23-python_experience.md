---
layout: single
title:  "[멋사] 1일차 Python 맛보기"
---


이번 포스팅은 멋쟁이사자처럼 8기를 진행하면서 진행한 교육을 정리했다. 


### 대신 반복하기


```python
import random

menu =["돈까스",'김밥',"피자","제육볶음"] 
# list: [] , 문자열, 숫자형, 모두 들어갈 수 있음. 
print(random.choice(menu))
```

    제육볶음
    


```python
import random
# 리스트 값 중에서 랜덤으로 값 1개 추출
print(random.choice(["된장찌개","피자","제육볶음","치킨","떡볶이"]))
```

    떡볶이
    


```python
# 반복문 : for
a = ["된장찌개","피자","치킨","떡볶이", '감자튀김']
for i in range(30):
    print(random.choice(a)) # 들여쓰기: 일반적으로 2, 4칸 활용 

print('이 문장은 반복되지 않습니다.') 
    
# DRY : Don't Repeat Yourself (직접 반복을 하지 말라.)
```

    피자
    된장찌개
    감자튀김
    떡볶이
    치킨
    피자
    치킨
    떡볶이
    감자튀김
    된장찌개
    된장찌개
    떡볶이
    치킨
    치킨
    감자튀김
    피자
    감자튀김
    치킨
    된장찌개
    떡볶이
    치킨
    떡볶이
    된장찌개
    피자
    피자
    피자
    피자
    피자
    된장찌개
    된장찌개
    이 문장은 반복되지 않습니다.
    


```python
# 무한루트 : while문 조건식이 true 일 경우에 계속해서 반복
import time

a = ["된장찌개","피자","치킨","떡볶이", '감자튀김']
while True:
    for i in range(10):
        print(random.choice(a))
        time.sleep(0.2)
    break  # 멈추기 
print('10개의 음식이 모두 출력되었습니다.')  
```

    감자튀김
    감자튀김
    치킨
    된장찌개
    피자
    피자
    된장찌개
    떡볶이
    된장찌개
    떡볶이
    10개의 음식이 모두 출력되었습니다.
    


```python
# 테이블 상자 만들기 : 데이블 상자에서 이름표는 변수의 역할
lunch = random.choice(["된장찌개","피자","제육볶음"])
dinner = random.choice(['피자','옛날소시지','피자','돈까스'])
lunch = '냉장고' # python은 다음과 같이 변수에 새로운 값을 넣으면 자동으로 기존의 값을 삭제하고, 새로운 값을 할당한다. 
lunch
```




    '냉장고'



### 딕셔너리(Dictionary) : 조립식 약통


```python
# 단순한 값을 저장하는 것이 아닌 key:value 형태로 데이터를 입력할 때는 {} 사용.
info = {'고향':'수원', '취미':'영화보기', '좋아하는 음식': '국수'} 
info
```




    {'고향': '수원', '취미': '영화보기', '좋아하는 음식': '국수'}



#### list, dictionary 고급


```python
information = {"고향":"수원", "취미":"영화관람","좋아하는 음식":"국수"}
foods = ["된장찌개", "피자", "제육볶음"]
```


```python
# key 값 추출
print(information.get('취미'))
# 새로운 값 생성하기
information['특기'] = '피아노' 
information['사는곳'] = '서울'
information
```

    영화관람
    




    {'고향': '수원', '취미': '영화관람', '좋아하는 음식': '국수', '특기': '피아노', '사는곳': '서울'}




```python
# 값 지우기
del information['좋아하는 음식']
information
```




    {'고향': '수원', '취미': '영화관람', '특기': '피아노', '사는곳': '서울'}




```python
# 값의 길이(개수) 추출
len(information)
```




    4




```python
# clear(): 딕셔너리값 모두 제거 
information.clear()
information
```




    {}




```python
# 리스트 값 추출 : indexing, slicing 

foods[0] # list의 1번째 값을 추출하라. 
foods[-1] # 뒤에서 첫번째 값을 추출하라.
foods[-2] # 뒤에서 두번째 값을 추출하라.

# append() : list에서의 값 추가
foods.append('김밥')
foods
```




    ['된장찌개', '피자', '제육볶음', '김밥', '김밥']




```python
# 삭제하기
del foods[-1]

foods
```




    ['된장찌개', '피자', '제육볶음', '김밥']



###  끝까지 반복하기 


```python
# 딕셔너리에서 for문을 활용한 값 추출
information = {'고향':'수원','취미':'영화관람','좋아하는 음식':'국수'}
for i,j in information.items():
    print(j) # j에는 value값만
#     print(i) # i에는 key값만
```

    수원
    영화관람
    국수
    

### 집합
    - list와 dictionary처럼 순서가 없음.
    - 중복 없음


```python
# 집합 생성하기 
foods = ['된장찌개','피자','제육볶음']
foods_set = set(foods)
foods_set
```




    {'된장찌개', '제육볶음', '피자'}



#### 집합 사용하기


```python
foods = ['된장찌개','피자','제육볶음','된장찌개']
foods_set = set(foods)
foods, foods_set # set은 중복이 제거됨을 확인.
```




    (['된장찌개', '피자', '제육볶음', '된장찌개'], {'된장찌개', '제육볶음', '피자'})




```python
# 합집합, 차집합, 교집합
menu1 = set(['된장찌개','피자','제육볶음'])
menu2 = set(['된장찌개','떡국','김밥'])

# 합집합
menu1 | menu2 # {'김밥', '된장찌개', '떡국', '제육볶음', '피자'}
# 차집합
menu1 - menu2 # {'제육볶음', '피자'}
# 교집합
menu1 & menu2
```




    {'된장찌개'}



### 만약에 , if 문


```python
'''
cond1. 리스트에서 메뉴하나를 뽑고, 
cond2. 만약 뽑힌 메뉴가 '제육볶음'이면, '곰배기로 주세요.'를 출력하시오.
cond3. 만약 제육볶음이 아니면, '그냥 주세요'를 출력하세요.

'''
import random

food = random.choice(['된장찌개','피자','제육볶음']) # cond1

if (food == '제육볶음'): 
    print(food, '곱배기로 주세요.')                 # cond2
else: 
    print(food,'그냥 주세요.')                     # cond3
    
```

    피자 그냥 주세요.
    

### 프로젝트 [오늘은 뭐 드실?] 제작하기


```python
lunch = ["된장찌개", "피자", "제육볶음", "짜장면"]

while True:
    print(lunch)
    item = input("음식을 추가 해주세요 : ")
    if item == "q":
        break
    else:
        lunch.append(item)
    
print(lunch)
set_lunch = set(lunch)


set_lunch = set(["된장찌개", "피자", "제육볶음", "짜장면"])
item = "짜장면"

set_lunch = set_lunch - set([item])
set_lunch
```

    ['된장찌개', '피자', '제육볶음', '짜장면']
    음식을 추가 해주세요 : 돈까스
    ['된장찌개', '피자', '제육볶음', '짜장면', '돈까스']
    음식을 추가 해주세요 : 국밥
    ['된장찌개', '피자', '제육볶음', '짜장면', '돈까스', '국밥']
    음식을 추가 해주세요 : q
    ['된장찌개', '피자', '제육볶음', '짜장면', '돈까스', '국밥']
    




    {'된장찌개', '제육볶음', '피자'}




```python
set_dinner = set(["된장찌개", "피자", "제육볶음", "짜장면"])
food = "짜장면"

set_dinner = set_dinner - set([food])

print(set_dinner)
```

    {'된장찌개', '제육볶음', '피자'}
    


```python
import random
import time

lunch = ["된장찌개", "피자", "제육볶음", "짜장면"]

while True:
    print(lunch)
    item = input("음식을 추가 해주세요 : ")
    if item == "q":
        break
    else:
        lunch.append(item)
    
print(lunch)


set_lunch = set(lunch) # 삭제 편의를 위해 집합으로 변환 
while True:
    print(set_lunch)
    item = input('삭제할 음식을 입력하시오. : ')
    if item == 'q':
        break
    else:
        set_lunch = set_lunch - set([item])

print(set_lunch, '중에서 선택합니다.')
print('5')
time.sleep(0.5)
print('4')
time.sleep(0.5)
print('3')
time.sleep(0.5)
print('2')
time.sleep(0.5)
print('1')
time.sleep(0.5)
print(random.choice(list(set_lunch))) 
```

    ['된장찌개', '피자', '제육볶음', '짜장면']
    음식을 추가 해주세요 : 돈까스
    ['된장찌개', '피자', '제육볶음', '짜장면', '돈까스']
    음식을 추가 해주세요 : 국밥
    ['된장찌개', '피자', '제육볶음', '짜장면', '돈까스', '국밥']
    음식을 추가 해주세요 : q
    ['된장찌개', '피자', '제육볶음', '짜장면', '돈까스', '국밥']
    {'돈까스', '짜장면', '된장찌개', '제육볶음', '피자', '국밥'}
    삭제할 음식을 입력하시오. : 피자
    {'돈까스', '짜장면', '된장찌개', '제육볶음', '국밥'}
    삭제할 음식을 입력하시오. : 국밥
    {'짜장면', '된장찌개', '돈까스', '제육볶음'}
    삭제할 음식을 입력하시오. : q
    {'짜장면', '된장찌개', '돈까스', '제육볶음'} 중에서 선택합니다.
    5
    4
    3
    2
    1
    된장찌개
    

 ### 함수 알아보기
     def 함수이름():
         함수에 들어가 내용1
         함수에 들어가 내용1

###  프로젝트2 [이상형이 뭐에요?]


```python
# key : value  = 질문 : 답변
total_dic = {}

while True:
    question = input("질문을 입력해주세요 : ")  # 질문을 받는다.
    if question == 'stop':                  
        break
    else:
        total_dic[question] = ""
        
for i in total_dic:
    print(i)
    answer = input("답변을 입력해주세요 : ")
    total_dic[i] = answer
print(total_dic)
```

    질문을 입력해주세요 : 이름이 뭔가?
    질문을 입력해주세요 : 나이가 어떻게 되는가?
    질문을 입력해주세요 : stop
    이름이 뭔가?
    답변을 입력해주세요 : 변민찬
    나이가 어떻게 되는가?
    답변을 입력해주세요 : 25
    {'이름이 뭔가?': '변민찬', '나이가 어떻게 되는가?': '25'}
    


```python
# key: value, key:value = '질문' : '질문내용', '대답':'대답내용'
total_list = []

while True:
    question = input("질문을 입력해주세요 : ")
    if question == "q":
        break
    else:
        total_list.append({"질문" : question, '답변':""})

for i in total_list:
    print(i['질문'])
    answer = input("답변을 입력해주세요 : ")
    i['답변'] = answer
print(total_list)

```

    질문을 입력해주세요 : 이름이 뭔가?
    질문을 입력해주세요 : 나이가 몇인가?
    질문을 입력해주세요 : q
    이름이 뭔가?
    답변을 입력해주세요 : 변민찬
    나이가 몇인가?
    답변을 입력해주세요 : 25
    [{'질문': '이름이 뭔가?', '답변': '변민찬'}, {'질문': '나이가 몇인가?', '답변': '25'}]
    
