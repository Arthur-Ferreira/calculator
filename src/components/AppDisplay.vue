<script>
export default {
  props: ['value']
}
</script>

<template>
  <div class="display">
    {{ value }}
  </div>
</template>

<style>
.display {
  grid-column: span 4;
  background-color: #0004;

  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 1.2rem;
  font-size: 2em;
  overflow: hidden;
}
</style>
