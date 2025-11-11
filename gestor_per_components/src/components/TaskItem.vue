<script setup>
// @ts-nocheck
import { defineProps, defineEmits } from "vue";
const props = defineProps({
  tasca: { type: Object, required: true },
  index: { type: Number, required: true }
});

const emit = defineEmits(["toggle-task", "delete-task"]);

function toggleRealitzada() {
  emit("toggle-task", props.index);
}

function eliminarTasca() {
  emit("delete-task", props.index);
}
</script>

<template>
  <li>
    <span :class="{ done: tasca.Realitzada }">{{ tasca.titol }}</span>
    <div class="botons">
      <button @click="toggleRealitzada">
        {{ tasca.Realitzada ? "Realitzada" : "Pendent" }}
      </button>
      <button @click="eliminarTasca">Esborrar</button>
    </div>
  </li>
</template>

<style scoped>
.done {
  text-decoration: line-through;
  color: #d291bc;
}
.botons {
  display: flex;
  gap: 5px;
}
button {
  background-color: #ffb6c1;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s ease;
}
button:hover {
  background-color: #ff99aa;
  transform: scale(1.05);
}
</style>
