<script setup>
import TodoItem from './TodoItem.vue';

const props = defineProps({
  todos: Array
})

const emit = defineEmits(['removeTodoInParent','transferEditToParent'])

const transferToParent = (id) => {
  emit('removeTodoInParent', id)
}

const transferEditTodo = (todo) => {
  emit('transferEditToParent', todo)
}

</script>

<template>
    <ul>
      <!-- {{ props.todos }} -->
        <TodoItem 
          v-for="(todo, index) in props.todos" 
          :key="index" 
          :todo="todo" 
          @removeTodo="transferToParent" 
          @editTodo="transferEditTodo"
          />
    </ul>
</template> 


<style scoped>

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}


</style>