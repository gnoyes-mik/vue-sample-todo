<template>
  <div class="container">
    <h2>To-Do List</h2>
    <input class="form-control" type="text" v-model="searchText" placeholder="Search">
    <hr/>
    <todoSimpleForm
        @add-todo="addTodo"
    />
    <div v-if="!filteredTodos.length">There is nothing to display!</div>
    <todoList
        :todos="filteredTodos"
        @toggle-todo="toggleTodo"
        @delete-todo="deleteTodo"
    />
  </div>
</template>

<script>
import {ref, computed} from 'vue';
import todoSimpleForm from "@/components/TodoSimpleForm";
import todoList from "@/components/TodoList";

export default {
  components: {
    todoList,
    todoSimpleForm
  },
  setup() {
    const todos = ref([]);
    const searchText = ref([]);
    const filteredTodos = computed(() => {
      if (searchText.value) {
        return todos.value.filter(todo => {
          return todo.subject.includes(searchText.value);
        });
      }
      return todos.value;
    });
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
      searchText,
      filteredTodos,
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