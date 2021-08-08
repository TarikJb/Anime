<template>
  <header>
    <h1>the<strong>anime</strong>database</h1>
    <form class="serach-box" @submit.prevent="handleAnime">
      <input
        type="search"
        class="search-field"
        id="search"
        placeholder="Search for an anime..."
        v-model="anime_query"
        required
      />
    </form>
  </header>
  <main>
    <div class="cards row" v-if="anime_list.length > 0">
      <Card v-for="anime in anime_list" :key="anime.mal_id" :anime="anime" />
    </div>
    <div class="non-results" v-else>
      <h3>Sorry, we have no result...</h3>
    </div>
  </main>
</template>

<script>
import { ref } from 'vue'
import Card from './components/Card'

export default {
  setup() {
    const anime_query = ref('')
    const anime_list = ref([])
    const handleAnime = async () => {
      anime_list.value = await fetch(
        `https://api.jikan.moe/v3/search/anime?q=${anime_query.value}`,
      )
        .then(res => res.json())
        .then(data => data.results)
        .catch(err => console.log(err))
      console.log(anime_list.value)
    }
    return {
      anime_query,
      anime_list,
      handleAnime,
    }
  },
  components: {
    Card,
  },
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  font-family: 'Fira Sans', sans-serif;
}

header {
  padding-top: 50px;
  padding-bottom: 50px;

  h1 {
    color: #888;
    font-size: 42px;
    font-weight: 400;
    text-align: center;
    text-transform: uppercase;
    margin-bottom: 30px;
    transition: 0.4s;

    strong {
      color: #313131;
    }

    &:hover {
      color: #313131;
    }
  }

  .serach-box {
    flex-wrap: wrap;
    text-align: center;

    .search-field {
      appearance: none;
      outline: none;
      border: none;
      background: #f3f3f3;
      box-shadow: 0px 4px 8px rgba(0px, 0px, 4px, 0.15);
      width: 100%;
      max-width: 600px;
      color: #313131;
      padding: 15px;
      border-radius: 8px;
      font-size: 20px;
      transition: 0.4s;

      &::placeholder {
        color: #aaa;
      }

      &:focus,
      &:valid {
        background-color: #313131;
        color: #fff;
        box-shadow: 0px 0px 0px rgba(0, 0, 0, 0.15);
      }
    }
  }
}

main {
  max-width: 1200px;
  margin: 0 auto;
  padding-left: 30px;
  padding-right: 30px;

  .cards {
    flex-wrap: wrap;
    display: flex;
    margin: 0 -8px;
  }
}
</style>
