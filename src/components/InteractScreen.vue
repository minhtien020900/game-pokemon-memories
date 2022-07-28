<template>
  <div class="screen">
    <div
      class="screen_inner"
      :style="{
        width: `${
          ((((this.heightBrowser - 16 * 4) / Math.sqrt(cardContext.length) -
            16) *
            3) /
            4 +
            16) *
          Math.sqrt(cardContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardContext"
        :key="index"
        :ref="`card-${index}`"
        :card="{ index, value: card }"
        :arrCardFlipped="arrCardFlipped"
        :cardsContext="cardContext"
        @onSelectCard="checkRule($event)"
      >
      </card-flip>
    </div>
  </div>
</template>

<script>
import CardFlip from "./Card";

export default {
  name: "InteractScreen",
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },

  data() {
    return {
      arrCardFlipped: [],
      heightBrowser: 0,
    };
  },
  components: {
    CardFlip: CardFlip,
  },
  mounted() {
    this.heightBrowser = document.querySelector(".screen").clientHeight;
  },
  methods: {
    checkRule(data) {
      if (this.arrCardFlipped.length === 2) return false;
      this.arrCardFlipped.push(data);
      if (this.arrCardFlipped.length === 2) {
        if (this.arrCardFlipped[0].value === this.arrCardFlipped[1].value) {
          this.$refs[`card-${this.arrCardFlipped[0].index}`][0].disableCard();
          this.$refs[`card-${this.arrCardFlipped[1].index}`][0].disableCard();
          this.arrCardFlipped = [];

          const disabledElements = document.querySelectorAll(".card.disabled");
          if (
            disabledElements &&
            disabledElements.length === this.cardContext.length - 2
          ) {
            setTimeout(() => {
              this.$emit("onFinish");
            }, 920);
          }
        } else {
          setTimeout(() => {
            this.$refs[`card-${this.arrCardFlipped[0].index}`][0].cardDown();
            this.$refs[`card-${this.arrCardFlipped[1].index}`][0].cardDown();
            this.arrCardFlipped = [];
          }, 800);
        }
      } else return false;
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  flex-wrap: wrap;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background: var(--dark);
  color: var(--light);
}
.screen .screen_inner {
  justify-content: center;
  display: flex;
  flex-wrap: inherit;
  margin: 2rem auto;
}
</style>
