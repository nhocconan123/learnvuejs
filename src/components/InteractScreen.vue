<template>
  <div class="scre">
    <!-- <h1>Interact Component here ...</h1> -->
    <card-screen
      v-for="(card, index) in cardsContext"
      :key="index"
      :cardsContext="cardsContext"
      :imgBackFaceUrl="`images/${card}.png`"
      :testCard="{ index, value: card }"
      ref="cards"
      @onFlip="checkRule"
      @onFlipBack="onFlipBackCard(index)"
    ></card-screen>
  </div>
</template>

<script>
import CardScreen from "./TestCard.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardScreen,
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (this.rules.length === 2) {
        if (this.rules[0].value === this.rules[1].value) {
          console.log("right");

          //add class 'disable' to component card
          this.$refs.cards[this.rules[0].index].onEnableDisableMode();
          this.$refs.cards[this.rules[1].index].onEnableDisableMode();
          this.rules = [];
        } else {
          console.log("wrong!");
          setTimeout(() => {
            this.$refs.cards[this.rules[0].index].onFlipBackCard();
            this.$refs.cards[this.rules[1].index].onFlipBackCard();
            this.rules = [];
          }, 800);
        }
      }
    },
    onFlipBackCard(index) {
      setTimeout(() => {
        this.$refs.cards[index].onFlipBackCard();
      }, 800);
    },
    onEnableDisableMode(index) {
      setTimeout(() => {
        this.$refs.cards[index].onEnableDisableMode();
      }, 800);
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}

.screen__inner {
  width: calc(424px);
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
