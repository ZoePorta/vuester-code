<template>
  <div>
    <p>
      {{ speak }}
    </p>
    <input
      type="text"
      v-show="this.dialogs[this.dialog].askName"
      v-model="playerName"
    />
    <button @click="changeDialog()" v-show="this.dialogs[this.dialog].game">
      NEXT
    </button>
    <button v-show="!this.dialogs[this.dialog].game">
      <router-link :to="{ name: 'Game' }">
        GO FIGHT THE MONSTER!
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
      playerName: "",
      dialog: 0,
      dialogs: [
        {
          text:
            "You wake up in the middle of a forest, remembering nothing. It looks like you are in another world, but it feels some way familiar.",
          game: true,
        },
        {
          text:
            "You walk to the mountains and find an old man near a cave. It looks like he is the only person arround, so you go to talk to him.",
          game: true,
        },
        {
          text: `— Holla, traveler! may i asketh f'r thy name?`,
          game: true,
          askName: true,
        },
        {
          text:
            "— Thee has't hath walked a very much long way to receiveth, and i knoweth wherefore!",
          game: true,
        },
        {
          text:
            "— Thou art looking f'r the treasure rumor'd to beest enshielf by the cockatrices in the cave. T wonneth't beest easy, i desire thou art eft.",
          game: false,
        },
      ],
    };
  },
  computed: {
    speak() {
      if (this.playerName) {
        this.dialogs[3].text = `— Ah aye! ${this.playerName} the famous treasure hunter, of course!
      I knoweth wherefore thee has't cometh hither! `;
      }
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
