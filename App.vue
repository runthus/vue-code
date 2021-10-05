<template>
  <div id="app">
     <TodoHeader></TodoHeader>
     <TodoInput v-on:addTodo="addTodo"></TodoInput>
     <TodoList v-bind:propsdata="todoItems"></TodoList>
     <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
// app.vue 에다가 4개의 컴포넌트를 불러와야 합니다.
// 모던 자바스크립트에서는 외부 js 파일을 불러오는 선언문 -> import
import Todoheader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';
export default {
  data() {
    return {
      todoItems: []
    }
  },
  created() {
    // 만약에 로컬 스토리지의 갯수가 0보다 크다면(데이터베이스에 데이터가 하나라도 들어있다면)
    // for문을 써서 배열형 변수 todoItems에다 데이터를 담아야 한다.
    if(localStorage.length > 0){
        for(var i=0; i < localStorage.length; i++){
          this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    addTodo(todoItem) {
      // 로컬 스트리지에 데이터를 추가하는 로직을 구현
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  components: {
     // TodoHeader 라는 컴포넌트 명을 주고 외부에서 받아온 TodoHeader.vue파일을 컴포넌트에 집어 넣는 작업
    'TodoHeader' : Todoheader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;500;700&display=swap');
  body {
    font-family: 'Ubuntu', 'san-selif';
    text-align: center;
    background-color: #f6f6f8;

  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
  }
</style>