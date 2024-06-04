<script setup>
</script>

<template>
    <li class="todo-item">
        <p>asdfasd</p>
        <button class="remove-btn">Remove</button>
    </li>
</template>


<style scoped>
button {
  padding: 8px 18px;
  margin: 0;
  cursor: pointer;
  transition: all ease 0.43s;
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