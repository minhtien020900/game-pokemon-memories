<template>
  <div class="screen">
    <card-flip
      v-for="(card, index) in cardContext"
      :key="index"
      :indexCard="card"
      :card="card"
      @onSelectCard="checkRule($event)"
    >
    </card-flip>
  </div>
</template>

<script>
import CardFlip from "./Card";

export default {
  name: "InteractScreen",
  props: {
    cardContext: {
      type: Array,
      default: () => {
        return [];
      },
    },
  },
  components: {
    CardFlip: CardFlip,
  },
  methods: {
    checkRule(event) {
      console.log(event);
    },
  },
};
</script>

<style scoped></style>
