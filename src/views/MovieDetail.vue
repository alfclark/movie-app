<template>
  <div class="movie-detail">
    <div class="detail-left">
      <img :src="movie.Poster" alt="Movie Poster" class="poster" />
    </div>
    <div class="detail-right">
      <h2 class="title">{{ movie.Title }}</h2>
      <div class="info">
        <p class="type">{{ movie.Type }}</p>
        |
        <p>{{ movie.Year }}</p>
        |
        <p>{{ movie.Genre }}</p>
        |
        <p>{{ movie.Rated }}</p>
        |
        <p>{{ movie.Runtime }}</p>
        |
        <p><i class="fa-solid fa-star"></i> {{ movie.imdbRating }}</p>
      </div>
      <p class="plot">{{ movie.Plot }}</p>
      <div class="director">
        <h3>Director</h3>
        <p class="name">{{ movie.Director }}</p>
      </div>
      <div class="actors">
        <h3>Actors</h3>
        <p class="name">{{ movie.Actors }}</p>
      </div>
    </div>
  </div>
  <div class="similar">
    <h2>Similar to this Film:</h2>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
/* import env from "@/env"; */

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        /* `http://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}` */
        `https://www.omdbapi.com/?apikey=732b5c43&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
          console.log(data);
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style>
.movie-detail {
  color: var(--white);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3rem;
}

.detail.left {
  width: 40%;
  display: inline-block;
}

.poster {
  border-radius: 1.5rem;
  width: 300px;
  height: 100%;
}
.detail-right {
  width: 60%;
  display: flex;
  flex-direction: column;
  margin-left: 2rem;
  gap: 1rem;
  justify-content: left;
  text-align: left;
  align-items: flex-start;
}
.title {
  font-size: 2rem;
}
.info {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}
.type {
  text-transform: capitalize;
}
.plot {
  font-size: 1rem;
}
.name {
  font-size: 1rem;
}

.similar {
  color: var(--white);
}
</style>
