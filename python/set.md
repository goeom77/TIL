# 부분집합

복습: No
작성일시: 2022년 8월 23일 오전 9:18

## 비트 연산자

```html
& : 비트 단위로 AND 연산
| : 비트 단위로 OR 연산
<< : 피연산자의 비트 열을 왼쪽으로 이동시킨다.
>> : 피연산자의 비트 열을 오른쪽으로 이동시킨다.
ex) n = 10
print(n<<1)  #10을 2배 한 값인 20 이 출력된다.
print(n>>1)  #10을 반으로 나눈 값인 5 가 출력된다.
print(n<<2)  #10을 4배 한 값인 40 이 출력된다.
print(n>>2)  #10을 반으로 나눈 후 다시 반으로 나눈 값인 2 가 출력된다.
```

- i&(1<<j) : i의 j번째 비트가 1인지 아닌지를 검사
    
    훨씬 짧게 쓸수 있기 때문에 사용함
    

```python
# 모든 부분집합을 표시하는 것
arr = list(map(int,range(N)))

n= len(arr)
for i in range(1<<n):
    for j in range(n):
        if i & (1<<j):
            print(arr[j], end=", ")
    print()
print()

```

## **부분집합 생성**

### **부분집합 합(Subset Sum) 문제**

- 유한 개의 정수로 이루어진 집합이 있을 때, 이 집합의 부분집합 중에서 그 집합의 원소를 모두 더한 값이 0이 되는 경우가 있는지를 알아내는 문제
- 예를 들어 [-7, -3, -2, 5, 8] 라는 집합이 있을 때, [-3, -2, 5]는 이 집합의 부분집합이면서 합이 0 이므로 이 경우의 답은 참이 된다.

### **부분집합의 수**

- 집합의 원소가 n개일 때, 공집합을 포함한 부분집합의 수는 2^n 개이다
- 이는 각 원소를 부분집합에 포함시키거나 포함시키지 않는 2가지 경우를 모든 원소에 적용한 경우의 수와 같다.
- 부분 집합 구하는 방법

```python
arr = [7, 2, 5, 3, 4, 3]
N =len(arr)

for i in range(N-1):
	minIdx = I
		for j in range(i+1, N):
			if arr[minIdx] > arr[j]:
				minIdx = j
		arr[minIdx], arr[i] = arr[i], arr[minIdx]
print(arr)
```

[부분집합 구하는 방법 이해하기 (2)](https://www.notion.so/b46a8fa2824e4a12b7b9aba724603ff6)

### 부분집합 구하기

---

- 자기자신을 포함한 모든 부분집합은 powerset이라고 한다. → 개수는 2^n개
- 백트래킹을 통한 powerset구하기
    1. 일반적인 백트래킹 접근 방법을 이용
    2. n개의 원소가 들어있는 집합의 2^n개의 부분집합을 만들 떄는, True 또는 False값을 가지는 항목들로 구성된 n개의 배열을 만드는 방법을 이용
    3. 여기서 배열의 i번째 항목은 i번째의 원소가 부분집합의 값인지 아닌지를 나타내는 값이다.

```python
def backtrack(a,k,input):
		global MAXCANDIDATES
		c = [0] * MAXCANDIDATES
		if k == input:
				process_solution(a,k) #답이면 원하는 작업을 한다
		else:
				k+=1
				ncandidates = construct_candidates(a,k,input,c)
				for i in range(ncandidates):
						a[k] = c[i]
						vacktrack(a,k,input)
```

- loop를 이용하여 부분집합을 생성하는 방법

```python
bit = [0,0,0,0]
for i in range(2):             # 0번째 원소
		bit[0] = i
		for j in range(2):         # 1번째 원소
				bit[1] = j
				for k in range(2):     # 2번째 원소
						bit[2] = k
						for l in range(2): # 3번째 원소
								bit[3] = l
								print(bit)     #생성된 부분집합 출력
```

```python
#  부분집합의 합이 10인 부분집합과 개수 구하기
def f(i, N):
    global  ans
    if i == N:
        s= 0
        for i in range(N):
            if bit[i]:
                s += A[i]
        if s == 10:                         
            ans += 1                        # 개수
            for i in range(N):
                if bit[i]:
                    print(A[i], end = ' ')  # 같은 부분집합끼리 모우기 위해서
            print()
    else:
        bit[i] = 1                          # 1은 넣은 경우 case1
        f(i+1, N)
        bit[i] = 0                          # 0을 넣은 경우 case2
        f(i+1, N)

A = [1,2,3,4,5,6,7,8,9,10]
bit = [0] * 10
ans = 0
f(0, 10)
print(ans)

```