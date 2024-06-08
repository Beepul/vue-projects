<script setup>
import { ref } from 'vue';
import {useToast} from 'vue-toast-notification';


const todo = ref({
  title: '',
  id: ''
})
const emit = defineEmits(['addNewTodo'])

const toast = useToast();

const handleTodoInput = () => {
  try {
    if(!todo.value.title){
      throw new Error('Title is required!')
    }

    todo.value.id = Date.now()

    emit('addNewTodo', {...todo.value}) 

    todo.value.title = ''
    todo.value.id = ''

  } catch (error) {
    toast.error(error.message)
  }
}

</script>


<template>
    <form @submit.prevent="handleTodoInput">
        <input type="text" v-model="todo.title" placeholder="Enter your task"/>
        <button type="submit" class="submit-btn">Add To Do</button>
    </form>
</template>


<style scoped>
button {
  padding: 8px 18px;
  margin: 0;
  cursor: pointer;
  transition: all ease 0.43s;
}
form{
  display: flex;
  align-items: center;
}
form input{
  flex: 1;
}
form input {
  margin: 0;
  padding: 8px 18px;
  box-sizing: border-box;
  border-radius: 4px 0 0 4px;
  border: 1px solid #b3b3b3;
}
form input:focus{
  outline: 1px solid rgb(43, 124, 245);
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


</style>