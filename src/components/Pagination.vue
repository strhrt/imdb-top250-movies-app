<template>
  <div class="movies__pagination overflow-auto">
    <b-pagination v-model="currentPageModel" :total-rows="total" :per-page="perPage" />
  </div>
</template>

<script>
export default {
  name: "Pagination",

  props: {
    currentPage: { type: Number, default: 1 },
    total: { type: Number, default: 1 },
    perPage: { type: Number, default: 1 },
  },
  computed: {
    currentPageModel: {
      get() {
        return this.currentPage;
      },
      set(value) {
        this.$emit("pageChanged", value);
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.movies__pagination {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}
.movies__pagination /deep/ .pagination .page-item .page-link {
  background-color: transparent;
  font-size: 14px;
  color: #fff;
  box-shadow: none;
  font-weight: bold;
}
.movies__pagination /deep/ .pagination .page-item.active .page-link {
  border-color: #fff;
  background-color: #fff;
  color: #000;
}
.movies__pagination /deep/ .pagination .page-item.disabled .page-link {
  color: gray;
}
</style>