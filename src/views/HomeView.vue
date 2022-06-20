<template>
  <div class="home">
    <div class="featured">Featured</div>
    <SearchBox />
  </div>
</template>

<script>
// @ is an alias to /src
import SearchBox from "@/components/SearchBox.vue";

export default {
  components: { SearchBox },
};
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  max-width: 100vw;
  align-items: center;
  justify-content: center;
}

.featured {
  color: var(--white);
  margin: 1rem;
}
</style>
