<template>
  <div class="card">
    <a :href="anime.url">
      <img :src="anime.image_url" :alt="anime.title + 'Poster'"
    /></a>
    <h3>{{ anime.title }}</h3>
  </div>
</template>

<script>
export default {
  props: ["anime"],
};
</script>

<style>
.card {
  flex: 1 1 32%;
  width: 32%;
  max-width: 32%;
  object-fit: cover;
  padding: 8px 8px;
  margin-bottom: 15px;
  transition: 0.4s;
}
.card:hover h3 {
  color: crimson;
}

.card a img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 15px;
  transition: 0.4s;
}
.card a img:hover {
  transform: scale(1.04);
}
h3 {
  padding: 15px;
  color: white;
  transition: 0.4s;
}

@media (max-width: 1350px) {
  .card {
    flex: 1 1 49%;
    width: 49%;
    max-width: 49%;
  }
}

@media (max-width: 900px) {
  .card {
    flex: 1 1 99%;
    width: 99%;
    max-width: 99%;
  }
}
</style>