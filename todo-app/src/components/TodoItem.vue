<script setup>
import { nextTick, ref } from 'vue';
import { useToast } from 'vue-toast-notification';

const {todo} = defineProps({
  todo: {
    title: String,
    id: Number
  },
})

const emit = defineEmits(['editTodo'])
const toast = useToast()

const show = ref(false)
const editTitle = ref(todo.title)
const inputRef = ref(null)


const handleEditTodo = () => {
  try {
    if(!editTitle.value){
      throw new Error('Title is required')
    }
    emit('editTodo', {title: editTitle.value, id: todo.id})
    show.value = !show.value
    
  } catch (error) {
    toast.error(error.message)
  }
}

const handleEditButton = async () => {
  show.value= true
  await nextTick();
  inputRef.value.focus()
}

const handleInputChange = (e) => {
  handleEditTodo()
}

</script>

<template>
    <li class="todo-item">
      <div class="todo-title-wrapper" v-if="show">
        <input class="todo-title" v-model="editTitle" ref="inputRef" @keyup.enter="handleInputChange">
        <button class="edit-submit-btn" @click="handleEditTodo">
          <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" fill="none">
            <path d="M16.19 2H7.81C4.17 2 2 4.17 2 7.81V16.18C2 19.83 4.17 22 7.81 22H16.18C19.82 22 21.99 19.83 21.99 16.19V7.81C22 4.17 19.83 2 16.19 2ZM16.78 9.7L11.11 15.37C10.97 15.51 10.78 15.59 10.58 15.59C10.38 15.59 10.19 15.51 10.05 15.37L7.22 12.54C6.93 12.25 6.93 11.77 7.22 11.48C7.51 11.19 7.99 11.19 8.28 11.48L10.58 13.78L15.72 8.64C16.01 8.35 16.49 8.35 16.78 8.64C17.07 8.93 17.07 9.4 16.78 9.7Z" fill="#292D32"/>
          </svg>
        </button>
      </div>
      <p v-else>{{ todo.title }}</p>
      <div class="actions">
        <button class="edit-btn" @click="handleEditButton" v-if="!show">
          <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24"><title/>
            <g id="Complete">
              <g id="edit">
                <g>
                  <path d="M20,16v4a2,2,0,0,1-2,2H4a2,2,0,0,1-2-2V6A2,2,0,0,1,4,4H8" fill="none" stroke="#000000" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/>
                  <polygon fill="none" points="12.5 15.8 22 6.2 17.8 2 8.3 11.5 8 16 12.5 15.8" stroke="#000000" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/>
                </g>
              </g>
            </g>
          </svg>
        </button>
        <button class="edit-btn" v-else @click="show=false">
          <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" width="20px" height="20px" viewBox="0 0 32 32" version="1.1">
            <title>cross-square</title>
            <desc>Created with Sketch Beta.</desc>
            <defs></defs>
              <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
                  <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-204.000000, -1035.000000)" fill="#000000">
                      <path d="M224.95,1046.05 C224.559,1045.66 223.926,1045.66 223.536,1046.05 L220,1049.59 L216.464,1046.05 C216.074,1045.66 215.441,1045.66 215.05,1046.05 C214.66,1046.44 214.66,1047.07 215.05,1047.46 L218.586,1051 L215.05,1054.54 C214.66,1054.93 214.66,1055.56 215.05,1055.95 C215.441,1056.34 216.074,1056.34 216.464,1055.95 L220,1052.41 L223.536,1055.95 C223.926,1056.34 224.559,1056.34 224.95,1055.95 C225.34,1055.56 225.34,1054.93 224.95,1054.54 L221.414,1051 L224.95,1047.46 C225.34,1047.07 225.34,1046.44 224.95,1046.05 L224.95,1046.05 Z M234,1063 C234,1064.1 233.104,1065 232,1065 L208,1065 C206.896,1065 206,1064.1 206,1063 L206,1039 C206,1037.9 206.896,1037 208,1037 L232,1037 C233.104,1037 234,1037.9 234,1039 L234,1063 L234,1063 Z M232,1035 L208,1035 C205.791,1035 204,1036.79 204,1039 L204,1063 C204,1065.21 205.791,1067 208,1067 L232,1067 C234.209,1067 236,1065.21 236,1063 L236,1039 C236,1036.79 234.209,1035 232,1035 L232,1035 Z" id="cross-square" sketch:type="MSShapeGroup"></path>
                  </g>
              </g>
          </svg>
        </button>
        <button class="remove-btn" @click="$emit('removeTodo', todo.id)">
          <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" fill="none">
            <path d="M4 6H20M16 6L15.7294 5.18807C15.4671 4.40125 15.3359 4.00784 15.0927 3.71698C14.8779 3.46013 14.6021 3.26132 14.2905 3.13878C13.9376 3 13.523 3 12.6936 3H11.3064C10.477 3 10.0624 3 9.70951 3.13878C9.39792 3.26132 9.12208 3.46013 8.90729 3.71698C8.66405 4.00784 8.53292 4.40125 8.27064 5.18807L8 6M18 6V16.2C18 17.8802 18 18.7202 17.673 19.362C17.3854 19.9265 16.9265 20.3854 16.362 20.673C15.7202 21 14.8802 21 13.2 21H10.8C9.11984 21 8.27976 21 7.63803 20.673C7.07354 20.3854 6.6146 19.9265 6.32698 19.362C6 18.7202 6 17.8802 6 16.2V6M14 10V17M10 10V17" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
      </div>
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
  padding: 20px 0;
  border-bottom: 1px solid #ccc;
  gap: 24px;
}

.todo-item:last-child{
  margin-bottom: 0;
  padding-bottom: 0;
  border: 0;
}

.todo-title-wrapper{
  flex: 1;
  display: flex;
  align-items: center;
  padding: 8px 12px;
  border-radius: 4px;
  border: 1px solid #ccc;
}
.todo-title-wrapper:has(.todo-title:focus){
  outline: 1px solid rgb(56, 233, 12)
}
.todo-title{
  flex: 1;
  border: 0;
}
.todo-title:focus{
  outline: none;
}

.edit-submit-btn{
  padding: 0;
  background-color: transparent;
  border: 0;
}


.remove-btn{
  border-radius: 0px;
  padding: 0;
  border: 0;
  background-color: transparent;
  margin-left: 6px
}
.remove-btn svg path{
  stroke:  rgb(242, 62, 62);
}
.remove-btn:hover {
  opacity: 0.7;
}
.remove-btn:focus {
  opacity: 1;
}

.edit-btn{
  border-radius: 0px;
  padding: 0;
  border: 0;
  background-color: transparent;
}
.edit-btn svg polygon{
  stroke:  rgb(56, 233, 12);
}
.edit-btn svg path{
  stroke:  rgb(56, 233, 12);
}
.edit-btn:hover {
  opacity: 0.7;
}
.edit-btn:focus {
  opacity: 1;
}

</style>