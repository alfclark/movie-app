<template>
  <form @submit.prevent="SearchMovies()" class="search-box">
    <input
      type="text"
      placeholder="What are you looking for?"
      v-model="search"
    />
    <button type="submit" value="search">
      <i class="fa-solid fa-magnifying-glass"></i>
    </button>
  </form>
  <div class="movies-list">
    <div class="movie-card" v-for="movie in movies" :key="movie.imdbID">
      <div class="links">
        <router-link
          :to="'/movie/' + movie.imdbID"
          class="movie-link"
          target="_blank"
        >
          <img class="poster" :src="movie.Poster" alt="Movie Poster" />
          <div class="detail">
            <h3 class="movie-title">{{ movie.Title }}</h3>
            <div class="info">
              <p class="type">{{ movie.Type }}</p>
              |
              <p class="year">{{ movie.Year }}</p>
            </div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
/* import env from "@/env"; */

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(
          /* `http://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}` */
          `http://www.omdbapi.com/?i=tt3896198&apikey=732b5c43&s=${search.value}`
        )
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
            console.log(movies.value);
          });
      }
    };
    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style scoped>
.search-box {
  background-color: var(--lightBlack);
  padding: 1rem;
  display: flex;
  gap: 1rem;
  border: solid 2px #f6f6f617;
  border-radius: 15px;
}

input {
  background-color: transparent;
  border: none;
  color: white;
  font-size: 1rem;
  font-weight: 400;
  appearance: none;
  outline: none;
}

button {
  color: var(--whiteLight);
  background-color: transparent;
  border: none;
  cursor: pointer;
}

button:hover {
  transform: scale(1.1);
  transition: 0.4s;
  color: white;
}

.movies-list {
  max-width: 100vw;
  margin-top: 2rem;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  justify-content: center;
  background-color: var(--darkBlack);
}

.movie-card {
  margin: 1rem;
  position: relative;
  display: inline-block;
  color: var(--white);
  border-radius: 1.5rem;
  -webkit-box-shadow: 0px 0px 54px -11px rgba(246, 246, 246, 0.1);
  -moz-box-shadow: 0px 0px 54px -11px rgba(246, 246, 246, 0.1);
  box-shadow: 0px 0px 54px -11px rgba(246, 246, 246, 0.1);
  cursor: pointer;
}

.movie-card:hover {
  transform: scale(1.1);
  transition: 0.4s;
}

.movie-link {
  color: var(--white);
}

.poster {
  width: 250px;
  height: 380px;
  border-radius: 1.5rem;
}

.detail {
  position: absolute;
  z-index: 1;
  margin: 0 auto;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 20%;
  padding: 1rem 0.5rem 1rem 0.5rem;
  background-color: var(--darkBlack);
  border-bottom-left-radius: 1.5rem;
  border-bottom-right-radius: 1.5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.info {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}
.movie-title {
  font-size: 1rem;
}
.type {
  text-transform: capitalize;
}
</style>
