<template>
  <div class="movie__item mb-3">
    <div class="movie__item__poster" :style="posterBg"></div>
    <div class="movie__item__info__wrap">
      <div class="movie__item__info">
        <h3 class="movie__item__info__title">{{movie.Title}}</h3>
        <span class="movie__item__info__year">{{movie.Year}}</span>
      </div>
      <div class="movie__item__controls row no-gutters">
        <div class="col pr-2">
          <b-button size="md" block variant="outline-light">Edit</b-button>
        </div>
        <div class="col pl-2">
          <b-button size="md" block variant="outline-light" @click="emitRemoveEvent">Remove</b-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieItem",
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  computed: {
    posterBg() {
      return {
        "background-image": `url(${this.movie.Poster})`,
      };
    },
  },
  methods: {
    emitRemoveEvent() {
      this.$emit("removeItem", {
        id: this.movie.imdbID,
        title: this.movie.Title,
      });
    },
  },
};
</script>

<style lang="sass" scoped>
.movie__item
  position: relative
  cursor: pointer
  border-radius: 5px
  overflow: hidden
  transition: all 0.2s ease-in
  height: 400px

  &:hover
    box-shadow: 0px 5px 30px rgba(0, 0, 0, 0.5)
    transform: scale(1.02)
  &:hover &__info__wrap
    opacity: 1
    background-color: rgba(0,0,0,0.7)
  &__poster
    position: absolute
    top: 0
    left: 0
    bottom: 0
    right: 0
    background-repeat: no-repeat
    background-position: center
    background-size: cover
    z-index: -99
  &__info__wrap
    padding: 20px 10px
    display: flex
    flex-flow: column nowrap
    justify-content: space-between
    height: 100%
    opacity: 0
    transition: all 0.2 ease-in
  &__info
    &__title
      font-size: 20px
      color: #fff
      &__year
        font-size: 16px
        color: #fff
</style>