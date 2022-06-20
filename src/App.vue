<template>
  <header>
    <router-link class="logo" to="/">
      <img src="./assets/logo.png" alt="logo" class="logoImg" />
      <h1 class="logoTitle"><span>movie</span>Zone</h1>
      <p>The place to find where to watch your movies.</p>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;500;700&display=swap");

:root {
  --darkBlack: #0c0d18;
  --lightBlack: #2b2b38;
  --white: #f6f6f6f1;
  --whiteLight: #f6f6f6b0;
  --mutedBlue: #2c3e50;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: var(--darkBlack);
  height: 100vh;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
}

.logo {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logoImg {
  width: 50px;
}

.logoTitle {
  color: var(--white);
  font-size: 1.5rem;
}

span {
  font-weight: 300;
}

p {
  color: var(--whiteLight);
  font-weight: 300;
  font-size: 0.7rem;
}
</style>
