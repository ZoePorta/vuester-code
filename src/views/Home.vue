<template>
  <div>
    <p>
      {{ speak }}
    </p>
    <button @click="changeDialog()" v-show="this.dialogs[this.dialog].game">
      NEXT
    </button>
    <button v-show="!this.dialogs[this.dialog].game">
      <router-link :to="{ name: 'Game' }">
        FIGHT!
      </router-link>
    </button>
  </div>
</template>

<script>
// @ is an alias to /src
/* import HelloWorld from '@/components/HelloWorld.vue' */

export default {
  name: "Home",
  data() {
    return {
      dialog: 0,
      dialogs: [
        { text: "Hello, traveller!", game: true },
        { text: "You've come so far.", game: true },
        { text: "I hope you are ready.", game: false },
      ],
    };
  },
  computed: {
    speak() {
      return this.dialogs[this.dialog].text;
    },
  },

  methods: {
    changeDialog() {
      this.dialog++;
    },
  },
};
</script>
