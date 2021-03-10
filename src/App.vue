<template>
  <div id="app">
    <spelling-test />
  </div>
</template>

<script>
import SpellingTest from "./components/SpellingTest";
export default {
  name: "spelling",
  components: { SpellingTest }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
