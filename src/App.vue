<template>
  <div class="container">
    <h2>To-Do List</h2>
    <todoSimpleForm @add-todo="addTodo"/>
    <div v-if="!todos.length">
      Todo list is empty!
    </div>
    <div v-for="(todo, index) in todos" :key="todo.id" class="card mt-2">
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input class="form-check-input" type="checkbox" v-model="todo.completed">
          <label class="form-check-label" :class="{ todo:todo.completed}">
            {{ todo.subject }}
          </label>
        </div>
        <div>
          <button class="btn btn-danger" @click="deleteTodo(index)">delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue';
import todoSimpleForm from "@/components/TodoSimpleForm";

export default {
  components: {
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
    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todos,
      todoStyle,
      addTodo,
      deleteTodo,
    };
  }
};
</script>

<style>
.todo {
  color: gray;
  text-decoration: line-through;
}
</style>