<template>
  <div class="p-2 divide-y">
    <div
      v-for="todo in props.todos"
      class="text-lg flex justify-between items-center font-semibold p-2 select-none cursor-pointer"
      :key="todo.id"
    >
      <TodoItem
        :todo="todo"
        :onDeletedTodo="() => emit('deleteTodo', todo)"
        :onUpdatedTodo="(newTodo) => emit('updateTodo', newTodo)"
      />
    </div>
  </div>
</template>

<script setup>
import TodoItem from "./TodoItem.vue";
const props = defineProps(["todos"]);
const emit = defineEmits(["deleteTodo", "updateTodo"]);

</script>
