# 1107

복습: No
작성일시: 2022년 11월 7일 오전 10:21

## ✨vuex

### 💡state management

여러개의 component를 조합해서 하나의 app을 만든다.

❗ Pass Props & Emit Event → 중첩이 깊어지면 데이터 전달이 쉽지 않음

🔅 중앙 저장소(store)에 데이터를 모아서 상태를 관리 → 계층에 상관없이 데이터 얻거나 변경할 수 있다. 즉, 규모가 크거나 컴포넌트 중첩이 깊은 프로젝트의 관리가 매우 편리 ➡ Vuex

### 💡Vuex

`vue create 이름`

`cd 이름`

`vue add vuex` : 를 통해 시작

✔  store 가 새로 생긴다.

![Untitled](1107%2025065bf012e645f79fd56a6a15fe39dd/Untitled.png)

- 색깔끼리 묶어서 생각
- 💡state
    - vue instance의 data에 해당
    - 중앙에서 관리하는 모든 상태 정보
    - state의 데이터가 변화하면 해당 데이터를 사용하는 component가 자동으로 다시 렌더링
    - $store.state로 state 데이터에 접근한다.
- 💡mutations
    - 실제로 **state를 변경**하는 유일한 방법
    - mutations 안에 함수를 handler함수라고 하는데 handler함수는 동기적이어야 한다.
        
        (state의 변화 시기를 특정할 수 없기 때문에)
        
    - 첫번째 인자는 state를 인자로 받고, component 혹은 Actions에서 commit()메서드로 호출됨
- 💡actions
    - 비동기 작업을 포함할 수 있다.
    - state를 직접 변경하지 않고, commit()메서드로 mutations를 호출해서 state를 변경한다.
        
        (state를 변경할 수 있지만 해서는 안됨)
        
    - component에서 dispatch() 메서드에 의해 호출됨

![Untitled](1107%2025065bf012e645f79fd56a6a15fe39dd/Untitled%201.png)

- 💡getters
    - vue instance의 computed에 해당
    - state를 활용하여 계산된 값을 얻고자 할 때 사용
    - getters의 결과는 캐시(cache)되며, 종속된 값이 변경된 경우에만 재계산
    - 첫번째 인자로 state, 두번째 인자 getter
    - getters에서 계산된 값은  state에 영향을 미치지 않는다.

cf ) 함수 축약형

![Untitled](1107%2025065bf012e645f79fd56a6a15fe39dd/Untitled%202.png)

### 💡데이터 조작

- 데이터 흐름 : **`component ➡ actions ➡ mutations ➡ state`**

```html
<template>
  <div id="app">
    <h1>{{message}}</h1>
  </div>
</template>
<script>
export default {
  name: 'App',
  components: {
  },
  computed: {
    message() {
      return this.$store.state.message
    }
  }
}
</script>
```

- context란
    
    ![Untitled](1107%2025065bf012e645f79fd56a6a15fe39dd/Untitled%203.png)
    

## ✨ Lifecycle Hooks

### 💡created

- vue instance가 생성된 후 호출
- 단,  mount 되지 않아 요소에 접근할 수 없다.
- ex) 이벤트가 발생하기 전에 함수를 불러오고 싶을 때
- axios를 가장 많이 사용한다.

### 💡mounted

- dom에 보여 줄 때

### 💡updated

- 새로운 자료가 뜰 때

### 💡부모 - 자식 간의 관계

- 부모 - 자식 관계에 따라 순서를 가지고 있지 않다. instance마다 각각의 lifecycle을 가지고 있기 때문

## ✨Todo with Vuex

pass

### 💡vuex-persistedstate

`npm i vuex-persistedstate` : 설치

```jsx
// index.js

import createPersistedState from 'vuex-persistedstate'

함수 안에 
plugins: [
		createPersistedState
],

```

vuex → 필요한 순간이 왔을 때 도입한다.