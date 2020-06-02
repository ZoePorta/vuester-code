<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'Home' }">Home</router-link> |
      <router-link :to="{ name: 'About' }">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: aliceblue;
  font-weight: bolder;
  background: #bb86ff;
  width: 100vw;
  height: 100vh;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #4444ff;
  text-shadow: 2px 2px 2px #ff50f0;
}

#nav a.router-link-exact-active {
  text-shadow: 2px 2px 2px #00e9a9;
}

p {
  padding: 1rem;
}
</style>
