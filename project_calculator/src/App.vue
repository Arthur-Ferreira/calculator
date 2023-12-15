<script>
import Calculator from './main/Calculator.vue'

export default {
  components: { Calculator }
}
</script>


<template>
  <h1>Calculator</h1>
  <Calculator />
</template>


<style>
@font-face {
  font-family: 'RobotoMono';
  src: url('./fonts/RobotoMono-Thin.ttf');
}

* {
  font-family: 'RobotoMono', monospace;
}

body {
  margin: 0;
}

#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  text-align: center;
  align-items: center;
  justify-content: center;

  color: #fff;
  background: linear-gradient(to right, rgb(83, 105, 118), rgb(41, 46, 73));
}
</style>
