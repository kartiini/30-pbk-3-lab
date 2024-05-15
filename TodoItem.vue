<template>
    <li>
      <input type="checkbox" v-model="todo.completed" @change="toggleCompleted(todo)" />
      <span :class="{ 'completed': todo.completed }">{{ todo.text }}</span>
      <button @click="editTodo">Edit</button>
      <button @click="deleteTodo">Delete</button>
    </li>
  </template>
  
  <script>
  import { defineComponent, ref } from 'vue';
  
  export default defineComponent({
    props: {
      todo: {
        type: Object,
        required: true
      }
    },
    emits: ['update', 'delete'],
    setup(props, { emit }) {
      const toggleCompleted = (todo) => {
        emit('update', { ...todo, completed: !todo.completed });
      };
  
      const editTodo = () => {
        emit('edit', props.todo);
      };
  
      const deleteTodo = () => {
        emit('delete', props.todo.id);
      };
  
      return {
        toggleCompleted,
        editTodo,
        deleteTodo
      };
    }
  });
  </script>
  
  <style scoped>
  .completed {
    text-decoration: line-through;
  }
  </style>
  