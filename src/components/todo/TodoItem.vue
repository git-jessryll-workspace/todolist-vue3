<template>
  <div class="flex items-center space-x-2">
    <svg
      v-if="!form.is_done"
      xmlns="http://www.w3.org/2000/svg"
      fill="none"
      viewBox="0 0 24 24"
      stroke-width="1.5"
      stroke="currentColor"
      class="w-6 h-6"
      @click="handleToggleDone"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
      />
    </svg>

    <svg
      v-else
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      fill="currentColor"
      class="w-6 h-6"
      @click="handleToggleDone"
    >
      <path
        fill-rule="evenodd"
        d="M2.25 12c0-5.385 4.365-9.75 9.75-9.75s9.75 4.365 9.75 9.75-4.365 9.75-9.75 9.75S2.25 17.385 2.25 12zm13.36-1.814a.75.75 0 10-1.22-.872l-3.236 4.53L9.53 12.22a.75.75 0 00-1.06 1.06l2.25 2.25a.75.75 0 001.14-.094l3.75-5.25z"
        clip-rule="evenodd"
      />
    </svg>
    <div v-if="!form.is_edited">
      {{ form.name }}
    </div>
    <div v-else>
      <input
        v-model="form.name"
        class="w-full p-2 text-lg"
        @keyup.enter="handleUpdateTodo"
      />
    </div>
  </div>

  <div class="flex space-x-2 items-center">
    <div
      class="cursor-pointer"
      @click="() => (form.is_edited = !form.is_edited)"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10"
        />
      </svg>
    </div>
    <div class="cursor-pointer" @click="handleDeleteTodo">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
        />
      </svg>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const form = ref({
  name: "",
  is_done: false,
  is_edited: false,
});
const props = defineProps(["todo", "onDeletedTodo", "onUpdatedTodo"]);

const { todo } = props;

onMounted(() => {
  form.value.name = todo.name;
  form.value.is_done = todo.is_done;
});

const handleDeleteTodo = async () => {
  props.onDeletedTodo(true);
};
const handleUpdateTodo = async () => {
  props.onUpdatedTodo({
    ...todo,
    name: form.value.name,
  });
  form.value.is_edited = false;
};

const handleToggleDone = async () => {
  form.value.is_done = !form.value.is_done;
  props.onUpdatedTodo({
    ...todo,
    is_done: !form.value.is_done,
  });
};
</script>
