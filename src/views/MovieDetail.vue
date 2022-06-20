<template>
  <div class="movie-detail">
    <h2>Movie Title</h2>
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
        `https://www.omdbapi.com/?i=tt3896198&apikey=732b5c43&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style></style>
