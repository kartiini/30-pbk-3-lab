<template>
    <ul>
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @update="updateTodo"
        @edit="editTodo"
        @delete="deleteTodo"
      />
    </ul>
  </template>
  
  <script>
  import { defineComponent } from 'vue';
  import TodoItem from './TodoItem.vue';
  
  export default defineComponent({
    components: { TodoItem },
    props: {
      todos: {
        type: Array,
        required: true
      }
    },
    emits: ['update', 'edit', 'delete'],
    setup(props, { emit }) {
      const updateTodo = (updatedTodo) => {
        emit('update', updatedTodo);
      };
  
      const editTodo = (todo) => {
        emit('edit', todo);
      };
  
      const deleteTodo = (todoId) => {
        emit('delete', todoId);
      };
  
      return {
        updateTodo,
        editTodo,
        deleteTodo
      };
    }
  });
  </script>
  