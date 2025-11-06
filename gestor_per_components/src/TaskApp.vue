<script setup>
// @ts-nocheck
import HeaderComponent from "./components/HeaderComponent.vue";
import { ref, computed } from "vue";

//ref es fa servir per strings i per crear arrays o objectes reactius
// Computed es fa servir per propietats derivades d'altres propietats reactives
const newTask = ref("");
const llista = ref([]);
const mostrarPendents = ref(false);
const Totals = computed(() => llista.value.length);
const Pendents = computed(
  () => llista.value.filter((tasca) => !tasca.Realitzada).length
);

function afegirTasca() {
  if (newTask.value.trim() !== "") {
    llista.value.push({ titol: newTask.value, Realitzada: false });
    newTask.value = ""; //neteja l'input
  }
}

function eliminarTasca(index) {
  llista.value.splice(index, 1);
}

const toggleRealitzada = (tasca) => {
  tasca.Realitzada = !tasca.Realitzada;
};

/* Computed: llista filtrada - > es fa servir el computed perque si fem servir una funcio normal aniria executant cada
cop que vue renderitza i així, el computed memoritza el resultat fins que canvia alguna de les seves dependències */
const llistaFiltrada = computed(() => {
  return mostrarPendents.value
    ? llista.value.filter((tasca) => !tasca.Realitzada)
    : llista.value;
});
</script>

<template>
  <HeaderComponent />

  <main>
    <h2>Gestiona les teves tasques:</h2>

    <form @submit.prevent="afegirTasca">
      <input
        v-model="newTask"
        type="text"
        @keyup.enter="afegirTasca"
        placeholder="Escriu una nova tasca"
      />
      <button type="submit">Afegir Tasca</button>
    </form>

    <h3>Llista de Tasques:</h3>
    <div class="mostra_pendents">
      <input type="checkbox" v-model="mostrarPendents" id="pendents" />
      <label for="pendents">Mostra només pendents</label>
      <p class="pendents" v-if="mostrarPendents">Tasques pendents:</p>
      <p class="missatge" v-if="Pendents === 0">(No hi ha tasques pendents)</p>

    </div>

    <p class="missatge" v-if="llista.length === 0">
      (introdueix tasques perque es mostrin aquí)
    </p>
    <ul>
      <li v-for="(tasca, index) in llistaFiltrada" :key="index">
        {{ tasca.titol }}

        <!-- Contenidor botons -->

        <div class="botons">
          <button @click="toggleRealitzada(tasca)">
            {{ tasca.Realitzada ? "Realitzada" : "Pendent" }}
          </button>
          <button @click="eliminarTasca(index)">Esborrar</button>
        </div>
      </li>
    </ul>

    <div class="totals">
     <h4> Totals: {{ Totals }} | Pendents: {{ Pendents }} </h4>


  <p class="missatge" style="color: green;" v-if="llista.length > 0 && Pendents === 0">
    Has acabat totes les tasques
  </p>

    </div>

  </main>
</template>

<style scoped>
* {
  font-family: "Audiowide", cursive;
}
h1,
h2,
h3 {
  color: rgb(186, 69, 96);
  text-align: center;
  margin: 0;
}

/* Main */
main {
  max-width: 500px;
  margin: 2rem auto;
  background-color: #fff0f5;
  padding: 1.5rem;
  border-radius: 15px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

/* Formulari */
form {
  display: flex;
  gap: 10px;
  margin-bottom: 1rem;
}

input[type="text"] {
  flex: 1;
  padding: 0.5rem;
  border: 2px solid #f4c2c2;
  border-radius: 10px;
  outline: none;
  font-size: 1rem;
}

input[type="text"]:focus {
  border-color: #f78da7;
}
/* Contenidor botons */
.botons {
  display: flex;
  gap: 5px; /* separació entre els botons */
}

/* Botons */
button {
  background-color: #ffb6c1;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

button:hover {
  background-color: #ff99aa;
  transform: scale(1.05);
}

/* Llista de tasques */
ul {
  list-style: none;
  padding-top: 20px;
  margin: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #ffe4e1;
  padding: 0.5rem 1rem;
  margin-bottom: 0.5rem;
  border-radius: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
}

li button {
  margin-left: 5px;
}

/* Text tatxat per tasques realitzades */
li span.done {
  text-decoration: line-through;
  color: #d291bc;
}

/* Contador de tasques */
div.counter {
  margin-top: 1rem;
  font-weight: bold;
  text-align: center;
  color: #c04848;
}

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

form {
  padding-top: 20px;
}
.totals {
  margin-top: 20px;
}
</style>
