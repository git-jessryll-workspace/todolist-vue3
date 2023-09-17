<template>
  <div class="p-2">
    <input
      class="w-full rounded-lg p-2 border border-gray-300"
      @keyup.enter="handleAddTodo"
      v-model="form.name"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
const emit = defineEmits(['addTodo'])

const form = ref({ name: "" });

const handleAddTodo = async ()  => {
    emit('addTodo', form);
    form.value.name = '';
}
</script>
