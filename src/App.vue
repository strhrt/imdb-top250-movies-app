<template>
  <div id="app">
    <PosterBg :poster="posterBg" />
    <MoviesList :list="moviesList" @changePoster="onChangePoster" />
  </div>
</template>

<script>
import MoviesList from "./components/MoviesList.vue";
import PosterBg from "./components/PosterBg";
import { mapActions, mapGetters } from "vuex";

export default {
  name: "App",
  components: {
    MoviesList,
    PosterBg,
  },
  data: () => ({
    posterBg: "",
  }),

  computed: {
    ...mapGetters("movies", ["moviesList"]),
  },
  methods: {
    ...mapActions("movies", ["fetchMovies"]),
    onChangePoster(poster) {
      this.posterBg = poster;
    },
  },
};
</script>

<style lang="sass">
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #2c3e50
  position: relative
</style>
