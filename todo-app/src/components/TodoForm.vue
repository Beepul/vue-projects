<script setup>
import { ref } from 'vue';

const title = ref('')

</script>


<template>
    <form @submit.prevent="$emit('addNewTodo', title)">
        <input type="text" v-model="title"/>
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
  margin-bottom: 20px;
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