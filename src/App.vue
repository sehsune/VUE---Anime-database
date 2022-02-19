<template>
  <div class="app">
    <header>
      <h1><span>Anime</span> Database</h1>
      <form class="search-box" @submit.prevent="HandleSearch">
        <input
          type="search"
          class="search-field"
          placeholder="Search for an anime..."
          v-model="search_query"
        />
      </form>
    </header>
    <main>
      <div class="cards">
        <Card v-for="anime in anime_list" :key="anime.mal_id" :anime="anime" />
      </div>
    </main>
  </div>
</template>

<script>
import { ref } from "vue";
import Card from "./components/Card.vue";
export default {
  components: { Card },
  setup() {
    const search_query = ref("");
    const anime_list = ref("");

    const HandleSearch = async () => {
      anime_list.value = await fetch(
        `https://api.jikan.moe/v3/search/anime?q=${search_query.value}`
      )
        .then((res) => res.json())
        .then((data) => data.results);
      search_query.value = "";
      console.log(anime_list.value);
    };

    return {
      Card,
      search_query,
      anime_list,
      HandleSearch,
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
body {
  background-color: #222;
  max-width: 50%;
  width: 50%;
  margin: 0 auto;
}

header {
  padding: 30px 40px;
}
header h1 {
  text-align: center;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 40px;
  color: #fff;
}
header h1 span {
  color: crimson;
}
.serach-box {
  padding: 10px 50px;
  margin: 20px auto;
}
.search-field {
  display: block;
  width: 100%;
  font-size: 25px;
  padding: 10px 10px;
  margin: 40px auto;
  border: none;
  border-radius: 10px;
}

main {
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px 20px;
}
.cards {
  display: flex;
  flex-wrap: wrap;
}
</style>
