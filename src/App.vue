<script setup>
import { ref } from "vue";
import { TodoForm, TodoList } from "./components/todo";

let todos = ref([]);

const addTodo = (form) => {
  const time = new Date().getTime();
  const newTodo = {
    name: form.value.name,
    id: time,
    is_done: false,
  };
  todos.value = [...todos.value, newTodo];
};
const updateTodo = (newTodo) => {
  todos.value = todos.value.map((item) => {
    if (item.id === newTodo.id) {
      return newTodo;
    }
    return item;
  });
};

const deleteTodo = (todo) => {
  todos.value = todos.value.filter((item) => item.id !== todo.id);
};
</script>

<template>
  <div class="flex justify-center">
    <div class="w-full md:w-1/2 border border-gray-300 p-2 rounded-lg mx-4 mt-6">
      <div class="flex justify-center py-2">
        <h1 class="text-2xl font-bold text-gray-700">Todo</h1>
      </div>
      <TodoForm @add-todo="addTodo" />
      <TodoList
        :todos="todos"
        @delete-todo="deleteTodo"
        @update-todo="updateTodo"
      />
    </div>
  </div>
</template>

<style scoped></style>
