<template>
  <div id="app">
    <header>
      <h1>Interactive Knowledge Map</h1>
    </header>
    <main>
      <!-- Include the Knowledge Map component -->
      <KnowledgeMap />
    </main>
  </div>
</template>

<script>
import KnowledgeMap from "./components/KnowledgeMap.vue";

export default {
  name: "App",
  components: {
    KnowledgeMap,
  },
};
</script>

<style>
/* Global styles */
#app {
  font-family: "Arial", sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  background-color: #f5f5f5;
  min-height: 100vh;
}

header {
  margin-bottom: 20px;
}

header h1 {
  font-size: 2.2rem;
  color: #333;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 10px;
}

main {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
