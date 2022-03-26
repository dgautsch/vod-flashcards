<template>

  <div class="row">

    <div class="container row">

        <div v-if="hasCurrentCard" class="vod-flashcard">

          <div
            class="vod-flashcard-front"
            :style="{ backgroundImage: `url(${currentCard.imageUrl})`}">

          </div>

          <div class="vod-flashcard-back">

            <p>{{currentCard.name}}</p>

          </div>

        </div>

        <div class="column" v-else>

          <h3>Would you like to start over?</h3>

          <button
            class="btn"
            @click="handleReset">Reset All Cards</button>

          <button
            class="btn"
            v-if="incorrectCards.length > 0"
            @click="useIncorrectCards">Restart with Incorrect Cards</button>

        </div>

    </div>

    <div v-if="hasCurrentCard" class="container row">

      <div class="column">

        <h3>Did you get it right?</h3>

        <button
          class="btn affirmative"
          @click="onCorrectClick">Yes</button>

        <button
          class="btn"
          @click="onIncorrectClick">No</button>

      </div>

    </div>

    <div class="container row">

      <div class="column column-correct">

        <h3>Correct Cards</h3>

        <ul class="vod-list" v-if="correctCards.length > 0">

          <li
            v-for="( correctCard, idx ) in correctCards"
            class="vod-list-item"
            :key="idx">✅ {{ correctCard.name }}
          </li>

        </ul>

      </div>

      <div class="column column-incorrect">

        <h3>Incorrect Cards</h3>

        <ul class="vod-list" v-if="incorrectCards.length > 0">

          <li
            v-for="( incorrectCard, idx ) in incorrectCards"
            class="vod-list-item"
            :key="idx">❌ {{ incorrectCard.name }}
          </li>

        </ul>

      </div>

    </div>

  </div>
</template>

<script>
export default {
  name: 'FlashCard',
  data() {
    return {
      publicPath: process.env.BASE_URL,
      cachedCards: [],
      cards: [{
        imageUrl: 'worship.png',
        name: 'worship',
      }, {
        imageUrl: 'commune.png',
        name: 'commune',
      }, {
        imageUrl: 'ascendant-plane.png',
        name: 'ascendant plane',
      }, {
        imageUrl: 'tower.png',
        name: 'tower',
      }, {
        imageUrl: 'hive.png',
        name: 'hive',
      }, {
        imageUrl: 'savathun.png',
        name: 'savathun',
      }, {
        imageUrl: 'fleet.png',
        name: 'fleet',
      }, {
        imageUrl: 'knowledge.png',
        name: 'knowledge',
      }, {
        imageUrl: 'darkness.png',
        name: 'darkness',
      }, {
        imageUrl: 'scorn.png',
        name: 'scorn',
      }, {
        imageUrl: 'guardian.png',
        name: 'guardian',
      }, {
        imageUrl: 'traveler.png',
        name: 'traveler',
      }, {
        imageUrl: 'love.png',
        name: 'love',
      }, {
        imageUrl: 'light.png',
        name: 'light',
      }, {
        imageUrl: 'give.png',
        name: 'give',
      }, {
        imageUrl: 'witness.png',
        name: 'witness',
      }, {
        imageUrl: 'grief.png',
        name: 'grief',
      }, {
        imageUrl: 'pyramid.png',
        name: 'pyramid',
      }, {
        imageUrl: 'drink.png',
        name: 'drink',
      }, {
        imageUrl: 'kill.png',
        name: 'kill',
      }, {
        imageUrl: 'enter.png',
        name: 'enter',
      }, {
        imageUrl: 'black-heart.png',
        name: 'black heart',
      }, {
        imageUrl: 'black-garden.png',
        name: 'black garden',
      }, {
        imageUrl: 'worm.png',
        name: 'worm',
      }, {
        imageUrl: 'stop.png',
        name: 'stop',
      }, {
        imageUrl: 'earth.png',
        name: 'earth',
      }],
      currentCard: {},
      correctCards: [],
      incorrectCards: [],
    };
  },
  created() {
    this.cachedCards = [...this.cards];
    this.getRandomCard();
  },
  computed: {
    hasCurrentCard() {
      return Object.keys(this.currentCard).length !== 0;
    },
  },
  methods: {
    getRandomCard() {
      const startingIndex = this.cards.length === 1
        ? 0 : Math.floor(Math.random() * this.cards.length);
      const currentCard = this.cards[startingIndex];
      this.cards.splice(startingIndex, 1);
      this.currentCard = currentCard;
    },
    onCorrectClick() {
      this.correctCards.push(this.currentCard);
      if (this.cards.length === 0) {
        this.currentCard = {};
        return;
      }
      this.getRandomCard();
    },
    onIncorrectClick() {
      this.incorrectCards.push(this.currentCard);
      if (this.cards.length === 0) {
        this.currentCard = {};
        return;
      }
      this.getRandomCard();
    },
    resetCards() {
      this.incorrectCards = [];
      this.correctCards = [];
      this.getRandomCard();
    },
    handleReset() {
      this.cards = [...this.cachedCards];
      this.resetCards();
    },
    useIncorrectCards() {
      this.cards = [...this.incorrectCards];
      this.resetCards();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
    position: relative;
    width: min(100% - 2rem, 70rem);
    margin-inline: auto;
}

.row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
}

.column {
  display: flex;
  flex-direction: column;
  flex-basis: 100%;
  flex: 1;
}

.column-incorrect,
.column-correct {
  border: none;
  padding: 1em;
}

h3 {
  text-align: center;
}

.vod-list {
  text-transform: capitalize;
  text-align: left;
}

.vod-flashcard {
  width: 300px;
  height: 200px;
  margin-inline: auto;
  transition: all 0.75s ease;
  transform-style: preserve-3d;
}

.vod-flashcard:hover {
  transform: rotateX(180deg);
}

.vod-flashcard-front, .vod-flashcard-back {
  /* This part controls the flip */
  backface-visibility: hidden;

  /* Size and card position */
  position: absolute;
  width: 300px;
  height: 200px;

  /* Appearance */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 4em;
  box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.3);
}

.vod-flashcard-front {
  background-repeat: no-repeat;
  background-size: 100%;
  background-color: #333;
  color: #fff;
}

.vod-flashcard-back {
  transform: rotateX(180deg);

  background-color: #fff;
  color: #333;
}

.vod-list {
  padding: 0;
  margin: 0;
}

.vod-list-item {
  list-style: none;
}

.btn {
  background-color: #282828;
  border-radius: 8px;
  border-style: none;
  box-sizing: border-box;
  color: #FFFFFF;
  cursor: pointer;
  flex-shrink: 0;
  font-size: 16px;
  font-weight: 500;
  height: 3rem;
  margin: 0 1em 0.5em;
  padding: 0 2.6rem;
  text-align: center;
  text-shadow: rgba(0, 0, 0, 0.25) 0 3px 8px;
  transition: all .5s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.btn.affirmative {
  background-color: #489;
}

.btn:hover {
  box-shadow: rgba(78, 73, 73, 0.5) 0 1px 10px;
  transition-duration: .1s;
}

</style>
