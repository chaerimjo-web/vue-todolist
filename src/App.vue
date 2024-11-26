<script setup>
import { reactive, ref } from 'vue';
import Todo from './components/TodoItem.vue';

const todoText = ref('');

const addtodo = (e)=>{ //엔터
  todoText.value = e.target.value;
  const todoTextLength =  todoText.value.trim().length;
  //빈 칸 없애기 -> 대상.trim()
  if(todoTextLength > 0 ){ //값이 있다면 length > 0
    todos.push({id:todoTextLength+1, title:todoText.value, checked:false})
  } //todos에 값을 넣음
  todoText.value = ''; //비우기
}
const todos = reactive([
  {id:1, title:'웹 배우기', checked:false}, //체크여부
  {id:2, title:'취직하기', checked:false}
])
const toggleCheckbox = (id, checked)=>{ //일치여부 대상.findIndex(각요소=>{return 조건}) 하나만 있으면 리턴 제거
  const idx = todos.findIndex(todo=> todo.id === id); //넘어온 아이디/ 투두의 아이디가 일치하면
  todos[idx].checked = checked
  console.log(id, checked, todos.values);
}

</script>

<template>
  <div id="app" class="container">
    <h1>Vue Todo App</h1>
    <BFormInput placeholder="할 일을 입력하세요" @keyup.enter="addtodo" v-model="todoText"/>
    <!-- v-model="todoText" -> 사용자가 입력한 값 value역할 -->
    <Todo
    v-for="todo in todos"
    :key="todo.id"
    :todo="todo"
    @toggle-checkbox="toggleCheckbox"
    />
  </div>
</template>

<style scoped>

</style>
