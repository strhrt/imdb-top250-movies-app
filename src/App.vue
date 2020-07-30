<template>
  <div id="app">
    <Loader />
    <PosterBg :poster="posterBg" />
    <Header />
    <MoviesList :list="moviesList" @changePoster="onChangePoster" />
    <Pagination
      :current-page="currentPage"
      :per-page="moviesPerPage"
      :total="moviesLength"
      @pageChanged="onPageChanged"
    />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import MoviesList from "@/components/MoviesList.vue";
import PosterBg from "@/components/PosterBg";
import Pagination from "@/components/Pagination";
import Loader from "@/components/Loader";
import Header from "@/components/Header";

export default {
  name: "App",
  components: {
    MoviesList,
    PosterBg,
    Pagination,
    Loader,
    Header,
  },
  data: () => ({
    posterBg: "",
  }),

  computed: {
    ...mapGetters("movies", [
      "moviesList",
      "currentPage",
      "moviesPerPage",
      "moviesLength",
    ]),
  },
  watch: {
    "$route.query": {
      handler: "onPageQueryChange",
      immediate: true,
      deep: true,
    },
  },
  methods: {
    ...mapActions("movies", ["changeCurrentPage"]),
    onChangePoster(poster) {
      this.posterBg = poster;
    },
    onPageChanged(page) {
      this.$router.push({ query: { page } });
    },
    onPageQueryChange({ page = 1 } = {}) {
      this.changeCurrentPage(Number(page));
    },
  },
};
</script>

<style lang="sass">
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  position: relative
</style>
