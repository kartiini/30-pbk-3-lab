<template>
  <div id="app">
    <h1>Vue To Do List</h1>
    <TodoForm :todo="currentTodo" @add="addTodo" @update="updateTodo" />
    <TodoList :todos="todos" @update="updateTodo" @edit="setCurrentTodo" @delete="deleteTodo" />
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue';
import TodoForm from './components/TodoForm.vue';
import TodoList from './components/TodoList.vue';

export default defineComponent({
  components: {
    TodoForm,
    TodoList
  },
  setup() {
    const todos = ref([]);
    const currentTodo = ref(null);

    const addTodo = (newTodo) => {
      todos.value.push(newTodo);
    };

    const updateTodo = (updatedTodo) => {
      const index = todos.value.findIndex(todo => todo.id === updatedTodo.id);
      if (index !== -1) {
        todos.value[index] = updatedTodo;
      }
      currentTodo.value = null;
    };

    const setCurrentTodo = (todo) => {
      currentTodo.value = todo;
    };

    const deleteTodo = (todoId) => {
      todos.value = todos.value.filter(todo => todo.id !== todoId);
    };

    return {
      todos,
      currentTodo,
      addTodo,
      updateTodo,
      setCurrentTodo,
      deleteTodo
    };
  }
});
</script>

<style>
#app {
  text-align: center;
  max-width: 600px;
  margin: auto;
}

ul {
  list-style-type: none;
  padding: 0;
}

button {
  margin-left: 5px;
}
</style>
