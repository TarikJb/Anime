<template>
  <div class="col-lg-4 col-md-6">
    <div class="card">
      <a target="_blank" :href="anime.url">
        <img
          :src="anime.image_url"
          :alt="'Anime Title : ' + anime.title"
          class="img-fluid rounded mx-auto d-block img-thumbnail"
        />
        <h3>{{ anime.title }}</h3>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: ['anime'],
}
</script>

<style scoped lang="scss">
.card {
  margin-bottom: 16px;
  transition: 0.4s;
  border: none;

  a {
    text-decoration: none;
  }

  img {
    height: 300px;
    object-fit: cover;
    border-radius: 16px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);
  }

  h3 {
    text-align: center;
    color: #313131;
    padding: 17px;
    transition: 0.4s;

    &:hover {
      color: #24c444;
    }
  }

  &:hover {
    transform: scale(1.05);
  }
}
</style>
