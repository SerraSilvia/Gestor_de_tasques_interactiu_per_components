<script setup>
// @ts-nocheck
import { ref, defineEmits } from "vue";

const emit = defineEmits(["add-task"]);
const newTask = ref("");

function afegirTasca() {
  const taskText = newTask.value.trim();
  if (taskText !== "") {
    emit("add-task", { titol: taskText, Realitzada: false });
    newTask.value = "";
  }
}
</script>

<template>
  <form @submit.prevent="afegirTasca">
    <input
      v-model="newTask"
      type="text"
      @keyup.enter="afegirTasca"
      placeholder="Escriu una nova tasca"
    />
    <button type="submit">Afegir Tasca</button>
  </form>
</template>
