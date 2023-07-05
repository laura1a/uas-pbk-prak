<template>
  <nav>
    <router-link to="/">Cuaca</router-link>|
    <router-link to="/lokasi">Lokasi</router-link>|
    <router-link to="/stopwatch">Stopwatch</router-link>|
    <router-link to="/tictactoe">Tic Tac Toe</router-link>|
    <router-link to="/foto">Foto</router-link>|
  </nav>
  <router-view/>
</template>

<style scoped>
#app {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: #333;
}

nav {
  padding: 30px;
  background-color: #f1f1f1;
}

nav a {
  font-weight: bold;
  color: #333;
  margin-right: 10px;
  text-decoration: none;
}

nav a.router-link-exact-active {
  color: #42b983;
}

nav a:hover {
  color: #42b983;
}

router-view {
  margin-top: 30px;
}
</style>
