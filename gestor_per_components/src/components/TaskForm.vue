<script setup>
// @ts-nocheck
import { defineEmits } from "vue";
// Creamos un emit para enviar la nueva tarea al componente padre
const emit = defineEmits(["add-task"]);

// Variable reactiva para el input
const newTask = ref("");

// Función para añadir tarea y enviar al padre
function afegirTasca() {
  const taskText = newTask.value.trim();
  if (taskText !== "") {
    // Emitimos la nueva tarea al componente padre
    emit("add-task", { titol: taskText, Realitzada: false });
    newTask.value = ""; // limpiar input
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


