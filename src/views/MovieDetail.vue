<template>
  <div class="detailed">
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
      <div class="movie-carousel">
        <div class="movies-list">
          <div class="movie-card" v-for="movie in movies" :key="movie.imdbID">
            <div class="links" v-show="movie.Poster != 'N/A'">
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
      </div>
    </div>
    <HomeFooter class="footer" />
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import HomeFooter from "@/components/HomeFooter.vue";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();
    const movies = ref([]);
    const title = ref({});

    onBeforeMount(() => {
      fetch(
        /* `http://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}` */
        `https://www.omdbapi.com/?apikey=732b5c43&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
          title.value = data.Title.split(" ")[0];
          console.log(title.value);
          fetch(
            /* `http://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}` */
            `https://www.omdbapi.com/?apikey=732b5c43&s=${title.value}&plot=full`
          )
            .then((response) => response.json())
            .then((data) => {
              movies.value = data.Search.slice(5);
              console.log(movies.value[0].Poster);
            });
        });
    });

    return {
      movie,
      movies,
      title,
    };
  },
  components: { HomeFooter },
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
  text-align: left;
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
  margin-bottom: 5rem;
}
.movieLinks {
  margin: 2rem 0;
}

.imdb {
  background-color: #e2b616;
  color: var(--darkBlack);
  padding: 1rem 2rem;
  border-radius: 2rem;
  border: var(--darkBlack) solid 2px;
  transition: 0.4s;
}
.imdb:hover {
  background-color: var(--darkBlack);
  color: #e2b616;
  border: var(--white) solid 2px;
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
  transition: 0.4s;
  cursor: pointer;
}

.movie-card:hover {
  transform: scale(1.1);
  -webkit-box-shadow: 0px 0px 54px -11px rgba(246, 246, 246, 0.3);
  -moz-box-shadow: 0px 0px 54px -11px rgba(246, 246, 246, 0.3);
  box-shadow: 0px 0px 54px -11px rgba(246, 246, 246, 0.3);
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
  height: 25%;
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
.footer {
  position: relative;
  bottom: 0;
  margin-top: 5rem;
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
    text-align: center;
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
