<template>
  <Quiz />
</template>

<script>
import Quiz from "./components/Quiz.vue";

export default {
  components: {
    Quiz,
  },
};
</script>

<style>
body {
  margin: 0px;
  padding: 0px;
  background: #0d4574;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
