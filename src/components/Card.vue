<template>
  <div class="card">
    <div
      class="card_inner"
      :class="{ ' is-flipped ': isFlipped }"
      @click="onToggle"
    >
      <div class="card_face card_face--front">
        <div class="card_content"></div>
      </div>
      <div class="card_face card_face--back">
        <div
          class="card_content"
          :style="{
            backgroundImage: `url(${require('@/assets/images/' +
              imageComputed)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    card: {
      type: [String, Number, Array, Object],
      required: true,
    },
    indexCard: {
      type: String,
    },
  },

  data() {
    return {
      isFlipped: false,
    };
  },
  computed: {
    imageComputed() {
      return this.indexCard + ".png";
    },
  },
  methods: {
    onToggle() {
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) {
        this.$emit("onSelectCard", this.card);
      }
    },
  },
};
</script>

<style scoped lang="css">
.card {
  display: inline-flex;
  margin-right: 1rem;
  margin-bottom: 1rem;
  width: 80px;
  height: 120px;
}

.card_inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  cursor: pointer;
  transform-style: preserve-3d;
  position: relative;
}

.card_inner.is-flipped {
  transform: rotateY(-180deg);
}

.card_face {
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  position: absolute;
  border-radius: 1rem;
  overflow: hidden;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card_face--back {
  transform: rotateY(180deg);
  background: var(--light);
}

.card_face.card_face--front .card_content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  height: 100%;
  width: 100%;
  background-size: 40px 40px;
}
.card_face.card_face--back .card_content {
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
  background-size: contain;
}
</style>
