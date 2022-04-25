<template>
  <div class="pagination">
    <ul class="pagination-list">
      <li
        class="page-item"
        :class="{ hidden: !hasFirst }"
      >
        <a class="page-link" @click="setPage(1)" @keydown="bar">1</a>
      </li>
      <li class="page-item" :class="{ hidden: !hasFirst }">...</li>
      <li
        v-for="page in pages"
        :key="page"
        class="page-item"
        :class="{ active: pager.currentPage === page }"
      >
        <a class="page-link" @click="setPage(page)" @keydown="bar">{{
          page
        }}</a>
      </li>
       <li class="page-item" :class="{ hidden: !hasLast }">...</li>
        <li class="page-item" :class="{ hidden: !hasLast }">
          <a class="page-link" @click="setPage(pager.totalPages)" @keydown="bar">
              {{ pager.totalPages }}</a>
        </li>
    </ul>
  </div>
</template>

<script>
import paginate from 'jw-paginate';

export default {
  props: {
    items: {
      type: Object,
      required: true,
    },
    initialPage: {
      type: Number,
      default: 1,
    },
    pageSize: {
      type: Number,
      default: 10,
    },
    maxPages: {
      type: Number,
      default: 10,
    },
    disableFirstLast: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      pager: {},
      pageRange: 1,
    };
  },
  created() {
    this.setPage(this.initialPage);
  },
  methods: {
    setPage(page) {
      const { items, pageSize, maxPages } = this;
      const newItems = items.map((item, index) => ({
        item,
        itemID: index + 1,
      }));
      const pager = paginate(newItems.length, page, pageSize, maxPages);
      const pageOfItems = newItems.slice(pager.startIndex, pager.endIndex + 1);
      this.pager = pager;
      this.$emit('changePage', pageOfItems);
    },
  },
  computed: {
    rangeStart() {
      const start = this.pager.currentPage - this.pageRange;
      return start > 0 ? start : 1;
    },
    rangeEnd() {
      const end = this.pager.currentPage + this.pageRange;

      return end < this.pager.totalPages ? end : this.pager.totalPages;
    },
    hasFirst() {
      return this.rangeStart !== 1;
    },
    hasLast() {
      return this.rangeEnd < this.pager.totalPages;
    },
    pages() {
      const pages = [];

      for (let i = this.rangeStart; i <= this.rangeEnd; i += 1) {
        pages.push(i);
      }
      return pages;
    },
  },
  watch: {
    items() {
      this.setPage(this.initialPage);
    },
  },
};
</script>

<style scoped>
.pagination {
  width: 100%;
  background-color: #000000;
  opacity: 0.9;
  position: sticky;
  bottom: 0px;
}

.pagination-list {
  display: flex;
  align-items: center;
  max-width: 320px;
  margin: 0 auto;
  padding-left: 0;
  justify-content: center;
}

.page-item {
  padding-left: 10px;
  padding-right: 10px;
  list-style-type: none;
  font-size: 14px;
  line-height: 60px;
  font-family: "Roboto Condensed", sans-serif;
  font-weight: 400;
  color: #ffffff;
}

.page-link {
  cursor: pointer;
}

.active {
  font-size: 18px;
  font-weight: 700;
}

.hidden {
  display: none !important;
}
</style>
