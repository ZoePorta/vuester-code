<template>
  <div>
    <!-- BARRAS DE VIDA -->
    <HPBars :playerHP="playerHP" :enemyHP="enemyHP"></HPBars>
    <!-- /BARRAS DE VIDA -->
    <!-- OPCIONES DEL JUEGO -->
    <Controls
      :healUses="healUses"
      :specialUses="specialUses"
      v-on:attack="attack"
      v-on:specialMove="specialMove"
      v-on:heal="heal"
      v-on:giveUp="giveUp"
    ></Controls>
    <!-- /OPCIONES DEL JUEGO -->

    <!-- LOGS -->
    <Logs :logs="logs" v-if="logs.length"></Logs>
    <!-- /LOGS -->
  </div>
</template>

<script>
import Controls from "@/components/Controls.vue";
import HPBars from "@/components/HPBars.vue";
import Logs from "@/components/Logs.vue";

//Importando Sweet Alert 2
import Swal from "sweetalert2";

export default {
  name: "Game",
  components: {
    Controls,
    HPBars,
    Logs,
  },
  data() {
    return {
      defaultPlayerHP: 80,
      defaultEnemyHP: 80,
      defaultHealUses: 5,
      defaultSpecialUses: 3,
      playerHP: null,
      enemyHP: null,
      healUses: null,
      specialUses: null,
      logs: [],
    };
  },
  methods: {
    setDefault() {
      this.playerHP = this.defaultPlayerHP;
      this.enemyHP = this.defaultEnemyHP;
      this.healUses = this.defaultHealUses;
      this.specialUses = this.defaultSpecialUses;
      this.logs = [];
    },
    attack() {
      let damage = this.calculateDamage(3, 10);
      this.enemyHP -= damage;
      this.enemyAttack();

      this.logs.unshift({
        text: `You inflict ${damage} damage points.`,
      });
    },
    calculateDamage(min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },
    enemyAttack() {
      let damage = this.calculateDamage(5, 12);
      this.playerHP -= damage;

      this.logs.unshift({
        text: `Monster inflicts ${damage} damage points.`,
      });
    },
    heal() {
      console.log(this.logs.length);
      if (this.playerHP < this.defaultPlayerHP / 2 && this.healUses > 0) {
        this.playerHP += 10;
        this.healUses--;

        this.logs.unshift({
          text: `You recover 10 HP points.`,
        });

        this.enemyAttack();
      } else if (this.playerHP >= this.defaultPlayerHP / 2) {
        Swal.fire({
          title: "You don't need this!",
          text: "Your HP level is pretty well :)",
          confirmButtonText: "Ok, I'll keep trying!",
        });
      } else {
        Swal.fire({
          title: "You can't do this anymore!",
          text: "You used all your heals :(",
          confirmButtonText: "Ok, I'll keep trying anyway",
        });
      }
    },
    specialMove() {
      if (this.specialUses > 0) {
        let damage = this.calculateDamage(8, 15);
        this.enemyHP -= damage;

        this.logs.unshift({
          text: `Your special move inflicts ${damage} damage points.`,
        });

        this.enemyAttack();
        this.specialUses--;
      }
    },
    giveUp() {
      Swal.fire({
        title: "Are you sure you want to give up?",
        text: "🐔🐔🐔🐔🐔🐔🐔🐔🐔🐔",
        confirmButtonText: "Yes, I peed my pants :(",
        showCancelButton: true,
        cancelButtonText: "No! I'm brave enough!",
      }).then((result) => {
        if (result.value) {
          this.goHome();
        }
      });
    },

    goHome() {
      this.$router.push("/");
    },

    finishGame() {
      this.$router.push("/inside-the-cave");
    },

    playerLoses() {
      this.playerHP = 0;
      Swal.fire({
        title: "You lose!",
        text:
          "You managed to scape and are now recovered. So is the monster. Would you try again?",
        confirmButtonText: "Yes, I can do it better!",
        showCancelButton: true,
        cancelButtonText: "No! I want to go home and cry :(",
      }).then((result) => {
        if (result.value) {
          this.setDefault();
        } else {
          this.goHome();
        }
      });
    },

    playerWins() {
      this.enemyHP = 0;
      Swal.fire({
        title: "You won!",
        text: "You killed the monster!",
        confirmButtonText: "I want my price!",
      }).then((result) => {
        if (result.value) {
          this.finishGame();
        }
      });
    },

    draft() {
      this.enemyHP = 0;
      this.playerHP = 0;
      Swal.fire({
        title: "You are on a draft!",
        text:
          "Neither of you can keep fighting. Maybe you can try again after a good rest. Would you?",
        confirmButtonText: "Yes, I can do it better!",
        showCancelButton: true,
        cancelButtonText: "No! I want to go home and cry :(",
      }).then((result) => {
        if (result.value) {
          this.setDefault();
        } else {
          this.goHome();
        }
      });
    },
  },

  watch: {
    playerHP: function() {
      if (this.playerHP <= 0) {
        this.playerLoses();
      }
    },
    enemyHP: function() {
      if (this.enemyHP <= 0) {
        if (this.playerHP <= 0) {
          this.draft();
        } else {
          this.playerWins();
        }
      }
    },
  },
  created() {
    this.setDefault();
  },
};
</script>

<style scoped></style>
