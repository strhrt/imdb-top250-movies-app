<template>
  <b-container>
    <h3 class="list__title">IMDb Top 250</h3>
    <b-row>
      <template v-if="isExist">
        <b-col cols="3" v-for="(movie, key) in list" :key="key">
          <MovieItem :movie="movie" @mouseover.native="onMouseOver(movie.Poster)" />
        </b-col>
      </template>
      <template v-else>
        <div>Empty list</div>
      </template>
    </b-row>
  </b-container>
</template>

<script>
import MovieItem from "./MovieItem";
export default {
  name: "MoviesList",
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  components: {
    MovieItem,
  },
  computed: {
    isExist() {
      return Boolean(Object.keys(this.list).length);
    },
  },
  methods: {
    onMouseOver(poster) {
      this.$emit("changePoster", poster);
    },
  },
};
</script>

<style lang="sass" scoped>
.list__title
  font-size: 50px
  margin-bottom: 30px
  color: #fff
</style>