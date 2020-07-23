<template>
  <div class="poster__page__bg" :style="posterStyle"></div>
</template>

<script>
export default {
  name: "Poster",
  props: {
    poster: { type: String, default: "" },
  },
  data: () => ({
    defaultPosterBg: "linear-gradient(45deg, rgb(0,3,38), rgb(82,15,117))",
  }),
  computed: {
    posterStyle() {
      return {
        "background-image": this.posterBg,
      };
    },
    posterBg() {
      return this.poster ? `url(${this.poster})` : this.defaultPosterBg;
    },
  },
};
</script>

<style lang="scss" scoped>
.poster__page__bg {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: -99;
  background-size: cover;
  background-position: center;
  transition: all 0.2s ease-in;
  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    opacity: 0.7;
    background-image: linear-gradient(45deg, rgb(0, 3, 38), rgb(82, 15, 117));
  }
}
</style>
