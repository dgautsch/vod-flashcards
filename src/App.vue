<template>
  <div class="container">
      <h1>Vow of the Disciple: Flashcards</h1>
      <p>
        <em>Hover over (tap on mobile) to reveal the card.
            Then select if you got the card right or wrong.
            You can restart with the cards you got wrong, or a fresh deck.
            Continue until the deck is empty.</em>
      </p>
      <FlashCard />
  </div>
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
.container {
    position: relative;
    width: min(100% - 2rem, 70rem);
    margin-inline: auto;
}
</style>
