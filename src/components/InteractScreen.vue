<template>
  <div class="scre">
    <h1>Interact Component here ...</h1>
    <card-screen
      v-for="(cards1, index) in cardsContext"
      :key="index"
      :cardsContext="cardsContext"
      :imgBackFaceUrl="`images/${cards1}.png`"
      :TestCard="{ index, value: cards1 }"
      :ref="`cards1-${index}`"
      @onFlip="checkRule($event)"
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
      if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("wrong!");
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`].onFlipBackCard();
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
//   methods: {
//     checkRule(card) {
//       console.log(card);
//       if (this.rules.length === 2) return false;
//       this.rules.push(card);
//       // console.log(this.rules);
//       if (
//         this.rules.length === 2 &&
//         this.rules[0].value === this.rules[1].value
//       ) {
//         console.log("right");
//       } else if (
//         this.rules.length === 2 &&
//         this.rules[0].value !== this.rules[1].value
//       ) {
//         console.log("wrong");

//         this.$refs[`card-${this.rules[0].index}`].onFlipBackCard();
//         this.rules = [];
//       } else return false;
//     },
//   },
// };
</script>
