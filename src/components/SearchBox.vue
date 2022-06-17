<template>
  <form @submit.prevent="" class="search-box">
      <input type="text" placeholder="What are you looking for?">
      <button type="submit" value="search"><i class="fa-solid fa-magnifying-glass"></i></button>
    </form>
</template>

<script>
export default {

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