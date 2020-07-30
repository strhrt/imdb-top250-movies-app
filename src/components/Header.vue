<template>
  <header class="header">
    <b-navbar class="navbar" type="dark" variant="dark">
      <b-container>
        <b-navbar-brand>MoviesDB</b-navbar-brand>
        <b-nav-form>
          <b-form-input
            v-model="searchValue"
            class="mr-sm-2 search__input"
            placeholder="Search"
            debounce="500"
          ></b-form-input>
        </b-nav-form>
      </b-container>
    </b-navbar>
  </header>
</template>

<script>
import { mapActions } from "vuex";
export default {
  name: "Header",
  data: () => ({
    searchValue: "",
  }),
  watch: {
    searchValue: "onSearchValueChanged",
  },
  methods: {
    ...mapActions("movies", [
      "searchMovies",
      "fetchMovies",
      "toggleSearchState",
    ]),
    onSearchValueChanged(val) {
      if (val) {
        this.searchMovies(val);
        this.toggleSearchState(true);
      } else {
        this.fetchMovies();
        this.toggleSearchState(false);
      }
    },
  },
};
</script>

<style lang="sass" scoped>
.header
   margin-bottom: 30px

.navbar
   background-color: rgba(0,0,0,0.7) !important
.search__input
   color: #fff
   background: rgba(255,255,255,0.1)
   border-color: rgba(255,255,255,0.4)
   &:focus
      box-shadow: none
      color: #fff
      background: rgba(255,255,255,0.2)
      border-color: rgba(255,255,255,0.4)
</style>