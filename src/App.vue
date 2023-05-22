<template>
  <v-app>
    <v-app-bar color="primary" title="Application Bar">
    </v-app-bar>
    <v-main style="min-height: 300px;">
      <router-view/>
    </v-main>
  </v-app>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-transform: uppercase;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
