<template>
  <div id="app">
    <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/css?family=Mitr"
    />
    <router-view />
  </div>
</template>

<script>
export default {
  components: {},
};
</script>

<style>
#app {
  font-family: "Mitr", serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: url(https://search-merchant.xn--42caj4e6bk1f5b1j.com/images/result-bg.png);
  background-size: cover;
  background-blend-mode: screen;
  padding: 0 20px 100px 20px;
}

#nav {
  color: white;
  padding: 20px;
}

#nav a {
  font-weight: bold;
  color: white;
}

#nav a.router-link-exact-active {
  font-weight: lighter;
}
@media only screen and (max-width: 768px) {
  #app {
    padding: 0;
  }
  body {
    font-size: 0.75rem;
  }
}
</style>

