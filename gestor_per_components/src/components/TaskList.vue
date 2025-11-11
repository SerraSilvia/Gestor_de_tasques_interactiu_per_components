<script setup>
// @ts-nocheck
import TaskForm from "./TaskForm.vue";
import TaskItem from "./TaskItem.vue";
import { ref, computed } from "vue";

const llista = ref([]);
const mostrarPendents = ref(false);

// Totales
const Totals = computed(() => llista.value.length);
const Pendents = computed(
  () => llista.value.filter(tasca => !tasca.Realitzada).length
);

const llistaFiltrada = computed(() =>
  mostrarPendents.value
    ? llista.value.filter(tasca => !tasca.Realitzada)
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
  <main>
    <h2>Gestiona les teves tasques:</h2>

    <!-- Formulario -->
    <TaskForm @add-task="addTask" />

    <!-- Filtro de pendientes -->
    <div class="mostra_pendents">
      <input type="checkbox" v-model="mostrarPendents" id="pendents" />
      <label for="pendents">Mostra només pendents</label>
      <p class="pendents" v-if="mostrarPendents">Tasques pendents:</p>
      <p class="missatge" v-if="Pendents === 0">(No hi ha tasques pendents)</p>
    </div>

    <!-- Mensaje si no hay tareas -->
    <p class="missatge" v-if="llista.length === 0">
      (Introdueix tasques perquè es mostrin aquí)
    </p>

    <!-- Lista de tareas -->
    <ul>
      <TaskItem
        v-for="(tasca, index) in llistaFiltrada"
        :key="index"
        :tasca="tasca"
        :index="index"
        @toggle-task="toggleTask"
        @delete-task="deleteTask"
      />
    </ul>

    <!-- Totales -->
    <div class="totals">
      <h4>Totals: {{ Totals }} | Pendents: {{ Pendents }}</h4>
      <p class="missatge" style="color: green;" v-if="llista.length > 0 && Pendents === 0">
        Has acabat totes les tasques
      </p>
    </div>
  </main>
</template>

<style scoped>
.mostra_pendents {
  font-size: 1rem;
  padding-top: 20px;
}
.pendents {
  color: rgb(186, 69, 96);
}
.missatge {
  color: #a9a9a9;
}
.totals {
  margin-top: 20px;
}
</style>
