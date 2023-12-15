<script>
export default {
  // Exports the Component
  props: ['value']
}
</script>

<template>
  <div class="display">
    {{ value }}
  </div>
</template>

<style>
:root {
  --bg-display: #0004;
}

.display {
  grid-column: span 4;
  background-color: var(--bg-display);

  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 1.2rem;
  font-size: 2em;
  overflow: hidden;
}
</style>
