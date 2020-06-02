<template>
  <div class="hpbars">
    <p>You</p>

    <div class="bar player" :style="{ width: playerHP + '%' }">
      {{ playerHP }}
    </div>
    <p>Monster</p>
    <div class="bar" :style="{ width: enemyHP + '%' }">
      {{ enemyHP }}
    </div>
  </div>
</template>

<script>
export default {
  name: "HPBars",
  props: {
    playerHP: Number,
    enemyHP: Number,
  },
};
</script>

<style scoped>
.hpbars {
  text-align: center;
}

.bar {
  background: #ff50f0;
  margin: auto;
  border-radius: 20px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 1rem;
}

.player {
  background: #00e9a9;
}
</style>
