<template>
  <div id="app">
    <spelling-test />
    <footer class="footer">
      <div class="content has-text-centered github-link">
        <p>
          GitHub repository
          <a
            href="https://github.com/eli-lavoie/vuejs-spellingtest"
            target="__blank"
          >
            here.
          </a>
        </p>
      </div>
    </footer>
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

body{
  min-height: 100vh;
  background-color: #fafafa;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 30px;
}

</style>
