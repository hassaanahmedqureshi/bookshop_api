<template>
  <BookCard />
</template>

<script>
import BookCard from "./components/book_card.vue";

export default {
  name: "App",
  components: {
    BookCard,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
