<template>
  <div class="">
    <main-screen
      @selectModeGame="onHandleBeforeStart($event)"
      v-if="statusMatch === 'default'"
    ></main-screen>
    <interact-screen
      :cardContext="settings.cardContext"
      v-else-if="statusMatch === 'match'"
      @onFinish="finishGame()"
    ></interact-screen>
    <result-screen
      v-else-if="this.statusMatch === 'result'"
      :timeFinish="timeFinish"
      @onStartAgain="onStartAgain"
    ></result-screen>
    <copy-right />
  </div>
</template>

<script>
import MainScreen from "./components/MainScreen";
import InteractScreen from "./components/InteractScreen";
import CopyRight from "./components/CoppyRight";
import "./assets/styles/global.css";

import { shuffled } from "./utils/array";
import ResultScreen from "./components/ResultScreen";
// import ResultScreen from "./components/ResultScreen";
export default {
  name: "App",
  components: {
    ResultScreen,
    InteractScreen,
    MainScreen,
    CopyRight,
  },
  data() {
    return {
      statusMatch: "default",
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null,
      },
      timeFinish: 0,
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
    finishGame() {
      this.timeFinish = new Date().getTime() - this.settings.startedAt;
      this.statusMatch = "result";
    },
    onStartAgain() {
      this.statusMatch = "default";
    },
  },
};
</script>

<style></style>
