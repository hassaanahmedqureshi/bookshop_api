<template>
  <AppNavbar class="header" />
  <AppBody />
  <AppFooter class="footer" />
</template>

<script>
import AppNavbar from "./components/AppNavbar.vue";
import AppFooter from "./components/AppFooter.vue";
import AppBody from "./components/AppBody.vue";

export default {
  name: "App",
  components: {
    AppNavbar,
    AppBody,
    AppFooter,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #f2f2f2;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
}

/* .footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: #ffffff;
} */
</style>
