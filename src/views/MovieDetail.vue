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
      <div class="movieLinks">
        <a
          class="imdb"
          :href="'https://www.imdb.com/title/' + movie.imdbID"
          target="blank"
          >See it on IMDb</a
        >
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
  margin: 1rem;
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
  text-align: left;
}
.title {
  font-size: 2rem;
  text-align: center;
}
.info {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}
.director,
.actors {
  text-align: left;
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

@media screen and (max-width: 900px) {
  .poster {
    width: 200px;
  }
  .detail-right {
    gap: 0.5rem;
  }
  .title {
    font-size: 1.5rem;
  }
  .plot {
    font-size: 0.8rem;
  }
  h3 {
    font-size: 1rem;
  }
  .name {
    font-size: 0.8rem;
  }
}
@media screen and (max-width: 500px) {
  .movie-detail {
    display: flex;
    flex-direction: column;
  }
  .poster {
    height: 300px;
  }
  .detail-right {
    gap: 0.5rem;
    justify-content: center;
    margin: 0;
  }
  .title {
    font-size: 1.5rem;
    margin-top: 1rem;
  }
  .info {
    justify-content: center;
  }
  .plot {
    font-size: 0.8rem;
  }
  .movieLinks {
    text-align: center;
  }
  h3 {
    font-size: 1rem;
  }
  .name {
    font-size: 0.8rem;
  }
}
</style>
