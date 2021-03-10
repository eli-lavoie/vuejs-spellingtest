<template>
  <div id="app">
    <spelling-test />
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
.github-link{
  padding-top: 5em;
}
</style>
