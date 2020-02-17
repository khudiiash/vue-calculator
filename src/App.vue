<template>
  <div id="app">
    <div class="left"></div>
    <div class="right"></div>
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    Calculator
  }
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  width: 100vw;
  height: 100vh;
}

.left {
  width: 35%;
  position: absolute;
  height: 100%;
  background: linear-gradient(
    to bottom right,
    rgb(53, 53, 53),
    rgb(18, 167, 159)
  );
  left: 0;
  top: 0;
  z-index: -1;
}
.right {
  width: 65%;
  position: absolute;
  height: 100%;
  right: 0;
  top: 0;
  background: linear-gradient(
    to bottom left,
    rgb(53, 53, 53),
    rgb(18, 167, 159)
  );
  z-index: -1;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #2c3e50;
  background: linear-gradient(rgba(124, 124, 124, 0.3), rgba(0, 0, 0, 0.3));
}
</style>
