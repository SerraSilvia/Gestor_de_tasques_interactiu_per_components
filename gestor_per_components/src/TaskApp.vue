<script setup>
// @ts-nocheck
import HeaderComponent from "./components/HeaderComponent.vue";
import TaskList from "./components/TaskList.vue";
</script>

<template>
  <HeaderComponent />
  <main>
    <TaskList />
  </main>
</template>

<style scoped>
* {
  font-family: "Audiowide", cursive;
}
h1, h2, h3 {
  color: rgb(186, 69, 96);
  text-align: center;
  margin: 0;
}

main {
  max-width: 500px;
  margin: 2rem auto;
  background-color: #fff0f5;
  padding: 1.5rem;
  border-radius: 15px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
</style>
