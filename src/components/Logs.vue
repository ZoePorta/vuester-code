<template>
  <div class="logs">
    <h2>LOGS</h2>
    <p v-for="log in logs" :key="log.id">
      {{ log.text }}
    </p>
  </div>
</template>

<script>
export default {
  name: "Logs",

  props: {
    logs: Array,
  },
};
</script>

<style scoped></style>
