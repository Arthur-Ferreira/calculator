<script>
export default {
  props: {
    label: {},
    operation: { type: Boolean },
    double: { type: Boolean },
    triple: { type: Boolean }
  }
}
</script>

<template>
  <button class="btn" 
  :class="{ double, triple, operation }">
    {{ label }}
  </button>
</template>

<style>
:root {
  --white: #fff;

  --bg-button: #f0f0f0;
  --bg-button-action: #ccc;
  --bg-button-ops: #fa8231;
  --bg-button-ops-action: #fa8231cc;
  --border-button: solid 1px #888;
}

.btn {
  font-size: 1.4em;
  background-color: var(--bg-button);
  border: none;
  border-right: var(--border-button);
  border-bottom: var(--border-button);
  outline: none;
}

.btn:active,
.btn:hover {
  background-color: var(--bg-button-action);
}

.btn.double {
  grid-column: span 2;
}

.btn.triple {
  grid-column: span 3;
}

.btn.operation {
  background-color: var(--bg-button-ops);
  color: var(--white);
}

.btn.operation:active,
.btn.operation:hover {
  background-color: var(--bg-button-ops-action);
}
</style>
