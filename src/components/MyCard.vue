<template>
  <div class="card">
    <a class="profile-link" :href="data.user.links.html" target="_blank">
      <div class="author">
        <img class="avatar" :src="data.user.profile_image.small" alt="avatar" />
        <div>
          <div class="user-name">{{data.user.name}}</div>
          <div class="user-account">{{`@${data.user.username}`}}</div>
        </div>
      </div>
    </a>
    <div class="photo-container">
      <img class="user-photo" :src="data.urls.regular" alt="avatar" />
    </div>
    <div class="views">{{data.likes}}</div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
    },
  },
};
</script>

<style scoped>
.card {
  margin-bottom: 8px;
  padding-top: 10px;
  max-width: 320px;
}

.card:nth-child(even) {
  margin-left: 20px;
}

.profile-link {
  display: inline-block;
  text-decoration: none;
  color: #8d8d8d;
}

.author {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  padding-left: 10px;
  text-decoration: none;
}

.avatar {
  margin-right: 10px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}

.user-name {
  margin-bottom: 3px;
  font-family: "Roboto Condensed", sans-serif;
  font-weight: 700;
  color: #333333;
}

.photo-container {
  margin-bottom: 10px;
  width: 320px;
  height: 230px;
}

.user-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.views {
  width: 60px;
  margin-left: auto;
  margin-right: 10px;
  background-image: url(".././assets/icons/eye.svg");
  background-repeat: no-repeat;
  background-position: right;
}

@media (max-width: 767px) {
  .card {
    max-width: 440px;
  }

  .card:nth-child(even) {
    margin-left: 0;
  }

  .photo-container {
    width: 440px;
    height: 330px;
  }
}

@media (max-width: 479px) {
  .card {
    margin-bottom: 16px;
  }
}

@media (max-width: 479px) {
  .card {
    max-width: 320px;
  }

  .photo-container {
    width: 320px;
    height: 230px;
  }
}
</style>
