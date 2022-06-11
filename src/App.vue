<template>
  <header>
    <router-link to="/">
      <h1><span>movie</span>Zone</h1>
    </router-link>
  </header>
  <router-view/>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;500;700&display=swap');

:root{
  --darkBlack: #0C0D18;
}

*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
  background-color: var(--darkBlack);
}


</style>
