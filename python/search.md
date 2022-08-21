# 🕶검색

복습: No
유형: algorism
작성일시: 2022년 8월 17일 오후 2:30

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

### 재귀호출

---

정의 :
- 자기 자신을 호출하여 순환 수행되는 것
- 함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출방식보다 재귀호출방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간단하게 작성가능

단점 : 일정 크기 이상인 경우 사용하지 않는다. 잘못된 경우 무한 루프의 오류에 빠질수 있다.

### Memoization

---

정의 :
- 재귀 함수로 구현한 알고리즘은 엄청난 중복 호출이 존재할 때 문제점이 있다.
- 메모이제이션은 컴퓨터 프로그램을 실행할 때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술, 동적 계획법의 핵심이 되는 기술이다.
- 'memoization'은 글자 그대로 해석하면 메모리에 넣기(to put in memory) 라는 의미이며 기억되어야 할 것 이라는 뜻의 라틴어 memorandum에서 파생되었다. 흔히 기억하기, 암기하기 등의 memorization과 혼동하지만 정확한 단어는 memoization이다. 동사형은 memoize이다.
- Memoization 방법을 적용한 알고리즘

```python
  # memo를 위한 배열을 할당하고, 모두 0으로 초기화한다
  # memo[0]을 0으로 memo[1]을 1로 초기화한다
  
  def fibo1(n):
      global memo
      if n >= 2 and len(memo) <= n:
          memo.append(fibo(n-1)) + fibo1(n-2))
      return memo[n]
  
  memo = [0, 1]    # 초기화
```

### DP(Dynamic Programming)이란?

---

- 동적 계획 알고리즘은 그리디 알고리즘과 같이 최적화 문제를 해결하는 알고리즘이다.
- 동적 계획 알고리즘은 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다

### DFS

---

- 비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요함
- 두 가지 방법
    - 깊이 우선 탐색(Depth First Search, DFS)
    - 너비 우선 탐색(Breadth First Search, BFS)
- 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법
- 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용

```python
visited = []        # 초기화
  stack = []
  def DFS(v):
      visited[v] = True
      while True:
          if (v의 인접 정점 중 방문 안한 정점 w가 있으면):
              stack.append(w)
              visited[w] = True;
          else:
              if stack: #(스택이 비어있지 않으면)
                  v = stack.pop() # 다시 출발
              else:
                  break # 갈곳이 업으면 break
  
  DFS(v)
```

### DFS - 인접관계

---

- 전부 딕셔너리에 지정하기
    
    ```python
    # 1
    database = {i: [] for i in range(1, V+1)}
    # 2
    from collections import defaultdict 
    ```
    

1번째 해결책 : 클래스로 만들자!

```python
class Graph():
		def __init__ (self, size):
				self.SIZE = size
				self.graph = [[0 for _ in range(size)] for _ in range(size)]
```

2번째 해결책 : SNA 라는 프로그램 사용

3번째 해결책 : 각각의 노드에 번호를 붙이고 문제를 해결하는 것

```python
adjList = 
[[1,2]   # 0에 인접인 애
,[0,3,4] # 1에 인접인 애
,[0,4]   # 2에 인접인 애
,[1,5]   # 3에 인접인 애
,[1,2,5] # 4에 인접인 애
,[3,4,6] # 5에 인접인 애
,[5]]    # 6에 인접인 애

def dfs(v,N):
		visited = [0] * N  # 정점의 개수
		stack = [0] *  N   # 스텍 생성  -- 방문한 지점에 되돌아 갈때 사용
		print(v)           # 방문!!
		top = -1           # stack을 stack의역할로 만들어 주는 도우미
		
		visited[v] = 1     # 시작점 방문 표시
		while True:
				for w in adjList[v]:      # if (v의 인접 정점 중 방문 안 한 정점 w가 있으면)
						 if visited[w] == 0: 
									top += 1        # push(v)
									stack[top] = v  
									v = w           # v <- w; ( w 에 방문)
									visited[w] = 1  # visited[w] <- true;
									print(v)        # 방문
									break
				else:                     # w가 없으면
							if top != -1:       # 스텍이 비어있지 않으면
									v = stack[top]  # pop
									top -= 1
							else:               # 스텍이 비어있으면
									break           # while
dfs(1, 7) # 1부터 가서 정점이 7인 경우
```

그래프 탐색 - 하나의 노드로부터 시작하여 차례대로 모든 노드들을 한번씩 방문하는 것, 많은 양의 데이터 중에서 원하는 데이터를 찾는 것

DFS, BFS의 방법이 있다.

깊이 우선 탐색 구현 - 방문 기준: 번호가 낮은 인접 노드부터 시작, 그래프에서 깊은 부분을 우선적 탐색

지정시 dict를 사용하는게 나을수도 있다. adjDict = {1:[2,3],2:[3,5]~~}

### String

---

코드체계 : 6비트면(64가지) 영어 대소문자를 모두 표현할 수 있다. 

→ 합쳐서 52가지 이므로 → ACSII코드 표준(1967년) 7비트로 공백을 비롯한 출력 가능한 문자 모두 표현

→ 다국어 처리를 위해 유니코드를 표준으로 마련

→ Character Set 으로 분류(UCS-2,UCS-4, → 인코딩의 필요성

→ 유니코드 인코딩(UTF-8,UTF-16(java),UTF-32(Unix)

- 문자열 분류
    
    ![캡처.PNG](%F0%9F%95%B6%E1%84%80%E1%85%A5%E1%86%B7%E1%84%89%E1%85%A2%E1%86%A8%20da48cd6823bc4b2b813da70e72a21c80/%25EC%25BA%25A1%25EC%25B2%2598.png)
    
- 문자열 메소드
    
    replace(), split(), isalpha(), find()
    

### Brute Force *(고지식한 패턴 검색 알고리즘)*

---

본문 문자열을 처음부터 끝까지 차례대로 순회→ 비효율

최대 시간 복잡도 : m = len(arr) → O(n*m)

- window(개별 lst)를 통해 각각 비교

```python
source = 'make a sentance'
for i in range(N):
	window = string =  source[i:i+m]

```

pattern 찾는 알고리즘 : 고지식한 비교(Brute Force), KMP , 보이어-무어 , 카프라법

### 보이어-무어 알고리즘

---

오른쪽에서 왼쪽으로 비교

대부분의 상용 소프트웨어에서 채택하는 알고리즘

window내에 찾는 문자열 없으면 문자 길이만큼 이동

### KMP

---

### 시저 암호, 부분집합의 합

---

```python
# 시저암호
def caesar(s, n):
    s = list(s)
    for i in range(len(s)):
        if s[i].isupper():
            s[i]=chr((ord(s[i])-ord('A')+ n)%26+ord('A'))
        elif s[i].islower():
            s[i]=chr((ord(s[i])-ord('a')+ n)%26+ord('a'))
 
    return "".join(s)
 
print(caesar("a B z", 4)) # 'e F d'
```

```python
# 부분 집합의 합
T = int(input())
for t in range(1,T+1):
    arr = list(map(int, input().split()))
    num = 10
    count = 0
    for i in range(1<<num):     # num의 부분함수 num개
        sum = 0
        for j in range(num):    # 원소의 수만큼 비트를 비교
            if i & (1<<j):      # i의 j번 비트가 1인경우
                sum += arr[j]   # j번 비트를 더한다.
        if sum == 0:            # 부분함수들의 합의 개수 계산
            count += 1
    count -= 1   # 공집합 제거
    if count > 0:
        result = 1
    else:
        result = 0
    print(f'#{t} {result}')
```