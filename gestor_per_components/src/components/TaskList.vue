<script setup>
// @ts-nocheck
import { ref, computed } from "vue";
import TaskForm from "./TaskForm.vue";
import TaskItem from "./TaskItem.vue";

const llista = ref([]); // lista de tareas
const mostrarPendents = ref(false); // filtrar solo pendientes

// Totales
const Totals = computed(() => llista.value.length);
const Pendents = computed(() => llista.value.filter(t => !t.Realitzada).length);

// Lista filtrada según checkbox
const llistaFiltrada = computed(() =>
  mostrarPendents.value
    ? llista.value.filter(t => !t.Realitzada)
    : llista.value
);

// Funciones para modificar la lista
function addTask(tasca) {
  llista.value.push(tasca);
}
function toggleTask(index) {
  llista.value[index].Realitzada = !llista.value[index].Realitzada;
}
function deleteTask(index) {
  llista.value.splice(index, 1);
}
</script>

<template>
  <!-- Formulario -->
  <TaskForm @add-task="addTask" />

  <!-- Filtro pendientes -->
  <div class="mostra_pendents">
    <input type="checkbox" v-model="mostrarPendents" id="pendents" />
    <label for="pendents">Mostra només pendents</label>
    <p class="pendents" v-if="mostrarPendents">Tasques pendents:</p>
    <p class="missatge" v-if="Pendents === 0">(No hi ha tasques pendents)</p>
  </div>

  <!-- Lista de tareas -->
  <ul v-if="llistaFiltrada.length">
    <TaskItem
      v-for="(tasca, index) in llistaFiltrada"
      :key="index"
      :tasca="tasca"
      :index="index"
      @toggle-task="toggleTask"
      @delete-task="deleteTask"
    />
  </ul>
  <p class="missatge" v-else>(Introdueix tasques perquè es mostrin aquí)</p>

  <!-- Totales -->
  <div class="totals">
    <h4>Totals: {{ Totals }} | Pendents: {{ Pendents }}</h4>
    <p class="missatge" style="color: green;" v-if="llista.length > 0 && Pendents === 0">
      Has acabat totes les tasques
    </p>
  </div>
</template>

<style scoped>
.mostra_pendents { font-size: 1rem; padding-top: 20px; }
.pendents { color: rgb(186, 69, 96); }
.missatge { color: #a9a9a9; }
.totals { margin-top: 20px; }
</style>
