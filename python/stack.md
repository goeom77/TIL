# 스택

복습: No
유형: algorism
작성일시: 2022년 8월 22일 오후 1:30

### 스택

---

- 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조
- 스택에 저장된 자료는 선형 구조를 갖는다
  - 선형구조 : 자료 간의 관계가 1:1의 관계를 갖는다
  - 비선형구조 : 자료 간의 관계가 1:N의 관계를 갖는다 (예 : 트리)
- 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다(LIFO)
- 마지막에 삽입한 자료를 가장 먼저 꺼냈다. 후입선출이라고 한다
  - 예를 들어 스택에 1,2,3 순으로 자료를 삽입한 후 꺼내면 3,2,1 순으로 꺼낼 수 있다

### 자료 구조

---

- 스택을 프로그램에서 구현하기 위해 필요한 자료구조와 연산
    - 자료구조 : 자료를 선형으로 저장할 저장소
        - 배열을 사용할 수 있다
        - 저장소 자체를 스택이라 부르기도 한다
        - 스택에서 마지막 삽인된 원소의 위치를 top`(stack pointer : sp)`이라 부른다
    - 연산
        - 삽입 : 저장소에 자료를 저장한다. 보통 push라고 부른다
        - 삭제 : 저장소에서 자료를 꺼낸다. 보통 pop이라고 부른다
        - 스택이 공백인지 아닌지를 확인하는 `연산.isEmpty` # 실제 내장된 함수 X
        - 스택의 top에 있는 item(원소)을 반환하는 `연산. peek` # 실제 내장된 함수 X
    - 스택 구현 고려 사항
      - 1차원 배열을 사용하여 구현할 경우 구현이 용이하다는 장점이 있지만 스택의 크기를 변경하기가 어렵다는 단점이 있다.
      - 이를 해결하기 위한 방법으로 저장소를 동적으로 할당하여 스택을 구현하는 방법이 있다. 동적 연결리스트를 이용하여 구현하는 방법을 의미한다. 구현이 복잡하다는 단점이 있지만 메모리를 효율적으로 사용한다는 장점을 가진다. 스택의 동적 구현은 생략

계산기

---

- 중위 표기법(infix notation) : 연산자를 피연산자의 가운데 표기하는 방법 1+ 2
- 후위 표기법(postfix notation) : 연산자를 피연산자 뒤에 표기하는 방법 1 2 +
- 중위 표기법을 후위 표기법으로 바꾸는 방법
    1. 괄호를 연산마다 붙힌다음 `)`뒤로 넘긴뒤에 괄호를 빼라
    2. 스택을 이용
        1. 중위 표기식에서 토큰 `(` 을 읽는다.
        2. 토큰이 연산자(number)이면 스택에 넣는다.
        3. 스택안의 우선 순위에 따라 높으면 push, 낮으면 pop → 여는 괄호가 나올 때 까지 pop() (`*` > `+` , `-` > `(`) 
        4. 연산할 때는 연산자 두개 꺼내서 연산하고 넣기(후기→ 연산방법)

### 백트래킹(Backtracking)기법

---

- 해 도중에 막히면 다시 돌아가서 해를 찾는 기법
- 최적화(optimization) 문제와 결정(decision)문제를 해결 할 수 있다.
- 활용
    - 미로찾기
        
        → 두가지 고르는 상황이면 스텍에 쌓기
        
    - n-Queen
    - Map Coloring
    - 부분 집합의 합
- 백트래킹과 깊이우선탑색 차이
    
    ```markdown
    1. 어떤 노드에서 출발하는 경로가 해결책으로 이어질 것 같지 않으면 
    그 경로를 따라가지 않음으로써 시도의 횟수를 줄임(Prunning 가지치기)
    2. 깊이우선탐색은 모든 경로를 추적하는데 비해 백트래킹은 불필요한 경로를 사전차단
    3. 깊이 우선탑색을 가하기에는 경우의 수가 너무 많음 -> N! 
    4. 백트래킹은 일반적으로 경우의 수가 줄어들지만 최악의 경우에는 여전히
    지수함수 시간을 요한다.
    ```
    
- 백트래킹 절차
    1. 상태 공간 트리의 깊이 우선 검색을 실시한다.
    2. 각 노드가 유망한지를 점검한다.
    3. 만일 그 노드가 유망하지 않으면, 그 노드의 부모 노드로 돌아가서 검색을 계속한다.
    
    ```python
    def checknode(v):
    	if promising(v):
    		if ther is a solution at v:   # 유망한 장소이니?
    			write the solution          # solution 기입
    		else:
    			for u in each chold of v:   # 탈락 -> 만약 다 안되면 다시 돌아가!
    				checknode(u)
    ```
    

### 부분집합 구하기

---

- 자기자신을 포함한 모든 부분집합은 powerset이라고 한다. → 개수는 2^n개
- 백트래킹을 통한 powerset구하기
    1. 일반적인 백트래킹 접근 방법을 이용
    2. n개의 원소가 들어있는 집합의 2^n개의 부분집합을 만들 떄는, True 또는 False값을 가지는 항목들로 구성된 n개의 배열을 만드는 방법을 이용
    3. 여기서 배열의 i번째 항목은 i번째의 우너소가 부분집합의 값인지 아닌지를 나타내는 값이다.

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

### 순열구하기

---

```python
#부분집합 1
# 합이 10인 부분집합 구하기
def f(i, N):
    global ans
    global cnt
    cnt+=1
    if i == N:
        s= 0                                  # 부분 집합의 합
        for i in range(N):
            if bit[i]:
                s += A[i]
        #         print(A[i], end = ' ')
        # print()
        if s == 10:
            ans += 1                          # 부분집합의 합이 10인 경우의 수
            # for i in range(N):
            #     if bit[i]:
            #         print(A[i], end = ' ')
            # print()
    else:
        candidate = [0,1]
        for x in candidate:
            bit[i] = x
            f(i+1,N)
        # bit[i] = 1
        # f(i+1, N)
        # bit[i] = 0
        # f(i+1, N)

A = [1,2,3,4,5,6,7,8,9,10]
bit = [0] * 10
ans = 0
cnt = 0
f(0, 10)
print(ans, cnt)
```

```python
#부분집합2
def f(i, N, s, t):
    global  answer
    global cnt
    cnt += 1
    if i == N:                  # 모든 원소가 고려된 경우
        if s == t:              # 부분집합의 합이 t면
            answer += 1
        return
    else:
        f(i+1, N, s+A[i], t)    # A[i]가 포함된 경우
        f(i+1, N, s, t)         # A[i]가 포함되지 않은 경우

A = [1,2,3,4,5,6,7,8,9,10]
bit = [0] * 10
cnt = 0
answer = 0
f(0, 10, 0, 10)
print(answer, cnt)
```