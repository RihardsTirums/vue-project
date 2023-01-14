<template>
  <div class="todo-container">
    <input class="input-todo" @input="updateInput" :value="state.inputValue" type="text" placeholder="What needs to be done?"/>
    <button class="add-todo-button" @click="addTodo">Add Todo</button>
  </div>

<ul>
  <select v-model="filter" class="select-design">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="incompleted">Incompleted</option>
    </select>
</ul>
<div v-for="(todo, index) in state.todos" :key="index">
    <span class="todo-number"></span>
    <TodoItem :task="todo.task" :isCompleted="todo.isCompleted" @deleteTodo="deleteTodo(index)"/>
  </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue';
import TodoItem from "../components/TodoItem.vue";

interface Todo {
  task: string;
  isCompleted: boolean;
}

const state = reactive({
  counter:0,
  inputValue: "",
  todos: [{
    task: "first task",
    isCompleted: false,
  }] as Todo[],
})

function updateInput(e: any){
  state.inputValue = e.target.value
}

function addTodo(){
  const newTodo = {
    task: state.inputValue,
    isCompleted: false,
  };
  state.todos.push(newTodo);
}
function deleteTodo(index: number){
  state.todos.splice(index,1);
  state.inputValue = "";
}
</script>

<style>
body{
  background: linear-gradient(#05833d, #222979);
  background-repeat: no-repeat;
}
.todo {
  display: flex;
  width: 25%;
  align-items: center;
  column-gap: 10px; /* gap between columns */
  margin-bottom: 10px; /* space between todos */
  padding: 5px 10px; /* space inside todo */
  background-color: #f9f9f9; /* background color */
  font-size:20px;
  font-weight:bold;
  text-align:center;
  background-color: rgb(31, 85, 73);
  color: rgb(192, 192, 192);
  border: 0.5px solid white;
  border-style: dotted;
  margin-left: 35px;
}
ul {
  list-style-type: none;
  counter-reset: todo-counter;
}
.todo-container{
   display: flex;
   align-items: center;
   margin-left: 40px ;
}
.todo-list {
  list-style-type: none;
  counter-reset: todo-counter;
}
.todo::before {
  counter-increment: todo-counter;
  content: counter(todo-counter) ") ";
  font-weight:bold;
}

.input-todo{
  width: 50%;
  height: 30px;
  border: 1px solid #ccc;
  padding: 5px 10px;
  font-size: 20px;
  margin-top: 20px;
  border-right:none ;
}
.add-todo-button{
  width: 100px;
  height: 42px;
  border: 1px solid #ccc;
  padding: 5px 10px ;
  margin-top: 20px;
  border-left: none;
  background-color: rgb(0, 20, 58);
  color: white;
}

.select-design{
  margin-bottom: 20px;
  width: 100px;
}
</style>