<template>
  <div class="">
    <main-screen
      @selectModeGame="onHandleBeforeStart($event)"
      v-if="statusMatch === 'default'"
    ></main-screen>
    <interact-screen
      :cardContext="settings.cardContext"
      v-else-if="statusMatch === 'match'"
    ></interact-screen>
    <coppy-right></coppy-right>
  </div>
</template>

<script>
import MainScreen from "./components/MainScreen";
import CoppyRight from "./components/CoppyRight";
import InteractScreen from "./components/InteractScreen";
import "./assets/styles/global.css";
import { shuffled } from "./utils/array";
// import ResultScreen from "./components/ResultScreen";
export default {
  name: "App",
  components: {
    InteractScreen,
    MainScreen,
    CoppyRight,
    // ResultScreen,
  },
  data() {
    return {
      statusMatch: "default",
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null,
      },
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      this.statusMatch = "match";

      //data ready
      this.settings.totalOfBlocks = config.totalOfBlocks;

      const firstCards = Array.from(
        {
          length: this.settings.totalOfBlocks / 2,
        },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];

      const cards = [...firstCards, ...secondCards];
      this.settings.cardContext = shuffled(shuffled(shuffled(shuffled(cards))));
      this.settings.startedAt = new Date().getTime();
    },
  },
};
</script>

<style></style>
