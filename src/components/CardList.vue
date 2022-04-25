<template>
  <div class="wrapper">
    <div class="card-list">
      <MyCard
        v-for="photo in pageOfItems"
        :key="photo.itemID"
        :data="photo.item"
      />
    </div>
  </div>
  <PaginationPage
    :items="photos"
    :pageSize="pageSize"
    @changePage="onChangePage"
  />
</template>

<script>
import MyCard from '@/components/MyCard.vue';
import PaginationPage from '@/components/PaginationPage.vue';
import axios from 'axios';

export default {
  components: {
    MyCard,
    PaginationPage,
  },
  data() {
    return {
      photos: [],
      pageOfItems: [],
      pageSize: 4,
    };
  },
  mounted() {
    this.getPhoto();
  },
  methods: {
    async getPhoto() {
      try {
        const response = await axios.get(
          'https://api.unsplash.com/photos/?client_id=lajPOuJ1AKjnkZFOcD_pdlSGrv719iUUeVuS5q0FP3w&per_page=30',
        );
        this.photos = Object.freeze(response.data);
      } catch (e) {
        alert('error');
      }
    },
    onChangePage(pageOfItems) {
      this.pageOfItems = [...pageOfItems];
    },
  },
};
</script>

<style scope>
.wrapper {
  margin: 0 auto;
  max-width: 660px;
  min-height: 700px;
}
.card-list {
  display: flex;
  flex-wrap: wrap;
}

@media (max-width: 767px) {
  .wrapper {
    max-width: 440px;
  }

  .card-list {
    flex-direction: column;
  }

}

@media (max-width: 479px) {
  .wrapper {
    max-width: 320px;
  }
}
</style>
