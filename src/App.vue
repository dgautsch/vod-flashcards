<template>
    <h1>Vow of the Disciple: Flashcards</h1>
    <FlashCard />
</template>

<script>
import FlashCard from './components/FlashCard.vue';

export default {
  name: 'App',
  components: {
    FlashCard,
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
