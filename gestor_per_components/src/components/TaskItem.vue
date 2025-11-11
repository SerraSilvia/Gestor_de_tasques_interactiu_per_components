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
    <button 
      :class="tasca.Realitzada ? 'realitzada' : 'pendent'" 
      @click="toggleRealitzada"
    >
      {{ tasca.Realitzada ? "Realitzada" : "Pendent" }}
    </button>
    <button @click="eliminarTasca">Esborrar</button>
  </div>
</li>

</template>

<style scoped>
/* li como contenedor flex */
li {
  display: flex;
  justify-content: space-between; /* texto izquierda, botones derecha */
  align-items: center;
  padding: 0.5rem 1rem;
  margin-bottom: 0.5rem;
  border-radius: 10px;
  background-color: #ffe4e1;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
  list-style: none; /* quita los puntos */
}

/* Texto de la tarea */
span {
  flex: 1; /* ocupa todo el espacio disponible */
}

/* Tachado si la tarea está realizada */
.done {
  text-decoration: line-through;
  color: #d291bc;
}

/* Botones alineados y separados */
.botons {
  display: flex;
  gap: 5px;
}

/* Estilo base de botones */
button {
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s ease;
}

/* Botón pendiente */
button.pendent {
  background-color: #ffb6c1;
}
button.pendent:hover {
  background-color: #ff99aa;
  transform: scale(1.05);
}

/* Botón realizada */
button.realitzada {
  background-color: #89c94dc9; /* verde */
}
button.realitzada:hover {
  background-color: #89c94dc9;
  transform: scale(1.05);
}
</style>

