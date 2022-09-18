<template>
  <div class="container">
    <h2>To-Do List</h2>
    <todoSimpleForm
        @add-todo="addTodo"
    />
    <div v-if="!todos.length">Todo list is empty!</div>
    <todoList
        :todos="todos"
        @toggle-todo="toggleTodo"
        @delete-todo="deleteTodo"
    />
  </div>
</template>

<script>
import {ref} from 'vue';
import todoSimpleForm from "@/components/TodoSimpleForm";
import todoList from "@/components/TodoList";

export default {
  components: {
    todoList,
    todoSimpleForm
  },
  setup() {
    const todos = ref([]);

    const todoStyle = ref({
      textDecoration: 'line-through',
      color: 'gray'
    });

    const addTodo = (todo) => {
      todos.value.push(todo);
    };

    const toggleTodo = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
    };

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todos,
      todoStyle,
      addTodo,
      toggleTodo,
      deleteTodo,
    };
  }
};
</script>

<style>
</style>