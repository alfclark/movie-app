<template>
  <form @submit.prevent="SearchMovies()" class="search-box">
    <input type="text" placeholder="What are you looking for?" v-model="search">
    <button type="submit" value="search">
      <i class="fa-solid fa-magnifying-glass"></i>
    </button>
  </form>
  <div class="movies-list">
    <div class="movie" v-for="movie in movies" :key="movie.imdbID">
      <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
        
      </router-link>
    </div>
  </div>
    
</template>

<script>
import { ref } from 'vue'
import env from '@/env'

export default {
setup() {
      const search = ref("");
      const movies = ref([]);

      const SearchMovies = () =>{
        if(search.value != ""){
          fetch(`http://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search
            search.value = ""
            console.log(movies.value);
          })
        }
      }
      return{
        search,
        movies,
        SearchMovies
        
      }
    },
}
</script>

<style scoped>
.search-box{
  background-color: var(--lightBlack);
  padding: 1rem;
  display: flex;
  gap: 1rem;
  border: solid 2px #f6f6f617;
  border-radius: 15px;
}


input{
  background-color: transparent;
  border: none;
  color: white;
  font-size: 1rem;
  font-weight: 400;
  appearance: none;
  outline: none;
}


button{
  color: var(--whiteLight);
  background-color: transparent;
  border: none;
  cursor: pointer;
}

button:hover{
  transform: scale(1.1);
  transition: .4s;
  color: white;
}

</style>