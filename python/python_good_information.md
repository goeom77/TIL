# 파이썬 꿀팁 모음

복습: No
유형: python
작성일시: 2022년 8월 13일 오전 9:31

### 개수에 안맞지만 할당하기

```python
a,*b=(1,2,3) #a=1, b=[2,3]
```

### 튜플을 딕셔너리의 키로 넣기

```python
a = dict()
a[(1,1)]=1
print(a) #{(1,1):2}
```

### 다중 반복문 한번에 탈출하기

```python
for i in range(10):
    for j in range(10):
        for k in range(10):
            print(i,j,k)
            if k==7:
                break
        else:
            continue
        break
    else:
        continue
    break
```

### 리스트 : 튜플의 원소 각각, 리스트의 원소 각각 고려해준다.

```python
list = [(2, 4), (1, 3), (3, 7), (1, 2), (6, 7), (3, 4), (4, 5)]

list.sort()

print(list)

# [(1, 2), (1, 3), (2, 4), (3, 4), (3, 7), (4, 5), (6, 7)]
```

### 무엇이든 더하는 sum 함수

```python
def Sum(*args):
    rst=type(args[0])()
    for i in args:
        rst+=i
    return rst
print(Sum(1,2,3))
print(Sum('a','b','c'))
print(Sum([1,2,3],[3,4,5]))
```