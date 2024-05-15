<template>
    <form @submit.prevent="handleSubmit">
      <input type="text" v-model="text" placeholder="What needs to be done?" />
      <button type="submit">{{ isEdit ? 'Update' : 'Add' }}</button>
    </form>
  </template>
  
  <script>
  import { defineComponent, ref, watch } from 'vue';
  
  export default defineComponent({
    props: {
      todo: {
        type: Object,
        default: null
      }
    },
    emits: ['add', 'update'],
    setup(props, { emit }) {
      const text = ref(props.todo ? props.todo.text : '');
  
      const handleSubmit = () => {
        if (props.todo) {
          emit('update', { ...props.todo, text: text.value });
        } else {
          emit('add', { text: text.value, completed: false, id: Date.now() });
        }
        text.value = '';
      };
  
      watch(() => props.todo, (newTodo) => {
        if (newTodo) {
          text.value = newTodo.text;
        } else {
          text.value = '';
        }
      });
  
      return {
        text,
        handleSubmit,
        isEdit: props.todo !== null
      };
    }
  });
  </script>
  