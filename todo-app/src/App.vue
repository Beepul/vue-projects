<script setup>
import { onMounted, ref } from 'vue';
import TodoForm from './components/TodoForm.vue';
import TodoList from './components/TodoList.vue';
import {useToast} from 'vue-toast-notification';


const todos = ref([])
const toast = useToast()

const handleNewTodo = (todo) => {
  todos.value.push(todo)
  localStorage.setItem('vue-todos',JSON.stringify(todos.value))
  toast.success('Todo added successfuly');
}

const handleRemoveTodo = (id) => {
  const newTodos = todos.value.filter((todo,i) => id !== todo.id)
  todos.value = newTodos
  localStorage.setItem('vue-todos',JSON.stringify(todos.value))
  toast.success('Todo removed successfuly');
}

const handleEditTodo = (todo) => {
  const newTodos = todos.value.map((tdo) => {
    if(tdo.id === todo.id){
      return todo 
    }else {
      return tdo
    }
  })

  todos.value = newTodos
  localStorage.setItem('vue-todos',JSON.stringify(todos.value))
  toast.success('Todo edited successfully')
}

onMounted(() => {
  const localStorageTodos = localStorage.getItem('vue-todos')
  if(localStorageTodos){
    todos.value = JSON.parse(localStorageTodos)
  }
})

</script>

<template>
  <main>
    <div class="todo-container">
      <TodoForm @addNewTodo="handleNewTodo" />
      <TodoList 
        :todos="todos" 
        @removeTodoInParent="handleRemoveTodo" 
        @transferEditToParent="handleEditTodo"
        />
    </div>
  </main>
</template>

<style scoped>
main{
  padding: 100px 0;
}
button {
  padding: 8px 18px;
  margin: 0;
  cursor: pointer;
  transition: all ease 0.43s;
}
.todo-container{
  padding: 28px 24px;
  border-radius: 4px;
  box-shadow: 0 0px 4px 4px #cccccc57;
  max-width: 450px;
  margin: 0 auto;
}
.todo-container form{
  display: flex;
  align-items: center;
}
.todo-container form input{
  flex: 1;
}
.todo-container form input {
  margin: 0;
  padding: 8px 18px;
  box-sizing: border-box;
  border-radius: 4px 0 0 4px;
  border: 1px solid #b3b3b3;
}
.submit-btn{
  border-radius: 0 4px 4px 0;
  border: 1px solid rgb(43, 124, 245);
  background-color: rgb(43, 124, 245);
  color: #fff;
}
.submit-btn:hover {
  background-color: transparent;
  color: rgb(43, 124, 245);
}
.submit-btn:focus {
  background-color: rgb(43, 124, 245);
  color: #fff;
}


ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}

.todo-item:last-child{
  margin-bottom: 0;
}

.remove-btn{
  border-radius: 4px;
  border: 1px solid rgb(242, 62, 62);
  background-color: rgb(242, 62, 62);
  color: #fff;
}
.remove-btn:hover {
  background-color: transparent;
  color: rgb(242, 62, 62);
}
.remove-btn:focus {
  background-color: rgb(242, 62, 62);
  color: #fff;
}

</style>
