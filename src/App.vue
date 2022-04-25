<template>
  <div class="app">
    <CardList />
  </div>
</template>

<script>
import CardList from '@/components/CardList.vue';
// import PaginationPage from "@/components/PaginationPage.vue";

export default {
  components: {
    CardList,
    // PaginationPage,
  },
};
</script>

<style>
@import "~normalize.css";

@font-face {
  font-family: "Roboto Condensed";
  src: url("https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@400;700&display=swap")
      format("woff2"),
    url("https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@400;700&display=swap")
      format("woff");
  font-display: auto;
  font-style: normal;
  font-weight: 400, 700;
}

* {
  box-sizing: border-box;
}

html,
body {
  height: 100%;
  width: 100%;
  background-color: #fff;
  font-size: 12px;
  line-height: 14px;
  color: #8d8d8d;
}
</style>
