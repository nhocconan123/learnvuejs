<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  ></main-screen>
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContact"
  ></interact-screen>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffled } from "./utils/array";
export default {
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContact: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
  },
  methods: {
    onHandleBeforeStart(config) {
      // console.log("running handle before star", config);

      //data ready
      this.settings.totalOfBlocks = config.totalOfBlocks;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      // console.log(firstCards);
      const secondCard = [...firstCards];
      const card = [...firstCards, ...secondCard];
      // console.log(card);
      this.settings.cardsContact = shuffled(card);
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },
  },
};
</script>
