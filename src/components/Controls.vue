<template>
  <div class="options">
    <button @click="attackEvent">
      ATTACK
    </button>
    <button @click="specialMoveEvent">SPECIAL MOVE ({{ specialUses }})</button>
    <button @click="healEvent">HEAL ({{ healUses }})</button>
    <button @click="giveUpEvent">
      GIVE UP
    </button>
  </div>
</template>

<script>
export default {
  name: "Controls",
  methods: {
    attackEvent() {
      this.$emit("attack");
    },
    specialMoveEvent() {
      this.$emit("specialMove");
    },
    healEvent() {
      this.$emit("heal");
    },
    giveUpEvent() {
      this.$emit("giveUp");
    },
  },
  props: {
    healUses: Number,
    specialUses: Number,
  },
};
</script>

<style scoped>
.options {
  width: 80%;
  padding: 1rem;
  margin: auto;
  margin-top: 1rem;
}
.options button {
  border: none;
  background: #4444ff;
  padding: 1rem;
  margin: 1rem;
  color: aliceblue;
  font-weight: bolder;
  border-radius: 1rem;
  border: 2px solid white;
}
</style>
