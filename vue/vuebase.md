# 1104


작성일시: 2022년 11월 4일 오전 8:29

### **vue pratice**

자식 ➡ 부모

- emit을 사용
    - 자식
    
    @click="ChildToParent" template에 넣으면 methods: {ChildToParent : function{ this.$emit('child-to-parent', 'child data')}} 부모 컴포넌트에게 child-to-parent라는 이벤트를 트리거
    
    두번째 인자는 데이터로써 같이 보낼수 있다.
    
    - 부모
    
    <자식명 @child-to-parent="parentGetEvent"/>로 상위 컴포넌트에서 청취 후
    
    methods:{parentGetEvent: function(){console.log('자식 컴포넌트에서 발생 이벤트')}} 이벤트에 맞춰 행동
    
    두번째 인자로 보낸 데이터는 function(inputData)로 받아 핸들러 함수의 인자로 사용 가능
    

부모 ➡ 자식(pass props)

- Static Prop

template안에 <자식명 msg = 'data'/> : msg="~"라는 property를 설정해준것

{{msg}} 자식에서 나오게 된다.

❗대신 자식의 props:{msg:String} 작성 필요

❗msg는 케밥케이스로 보낼 필요

- Dynamic Prop
    
    template안에 <자식명 :dynamic-props = 'abC'/> : dynamic-props ="abC"라는 property를 설정해준것
    
    부모의 data : function () { return {abC : '~'}}
    
    자식에서는 static과 동일
    

### **props 종류**

- Array
- String
- Object

### **script 종류**

- name : 파일 이름 ex) name: 'TodoList'
- components : 자식 이름 ex) componenets : { TodoList }
- data : 해당 페이지에서 보관할 정보
- props :
- methods : 함수

### **input**

- type : input 방식
- v-model="childInputData" : data: function(){return{childInputData:null}}
    
    data로 childInputData의 값이 들어간다.
    
- @keyup.enter="childInput" : methods: {childInput:function(){this.$emit('child-input',this.childinputData)}}
- @input = 'inputData' : input값이 들어오면 inputData를 수행하기
