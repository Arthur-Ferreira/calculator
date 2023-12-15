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
:root {
  --white: #fff;

  --bg-app-light: #536976;
  --bg-app-dark: #292e49;
}

* {
  font-family: monospace, sans-serif;
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

  color: var(--white);
  background: linear-gradient(to right, var(--bg-app-light), var(--bg-app-dark));
}
</style>
