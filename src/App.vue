<template>
 <h1>Vue Todo App</h1>
 <form @submit.prevent="addNewTodo">
   <label>Task</label>
   <input v-model="newTodo" name="newTodo">
   <button>Add Task</button>
 </form>
 <ul>
  <button @click="markAllDone">All Done</button> 
  <button @click="removeAll">Remove All</button> 
 <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
   <h4 :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h4>
    <button @click="removeTodo(index)">Remove</button>
 </li>
 </ul>
</template>

<script>
import {ref} from 'vue'

export default {
  setup() {

    const newTodo = ref('')
    const todos = ref([])

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done:false,
        content: newTodo.value
      })
      newTodo.value = ''
    }

    function toggleDone(todo) {
      todo.done = !todo.done
    }

    function removeTodo(index) {
      todos.value.splice(index, 1)
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true )
    }

    function removeAll() {
      todos.value = []
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAll
    }
  }
  
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}

.todo {
  cursor: pointer;
}
</style>
