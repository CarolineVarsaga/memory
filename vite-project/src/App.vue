<script setup lang="ts">
  import { ref } from 'vue';

  interface Card {
    symbol: string; 
    flipped: boolean; 
    matched: boolean; 
  }

  const cards = ref<Card[]>([]);
  const flippedCards = ref<{ index: number; card: Card }[]>([]);

  const flipCard = (index: number) => {
    const card = cards.value[index];
    if (card.flipped || card.matched || flippedCards.value.length === 2) {
      return;
    }

    card.flipped = true;
    flippedCards.value.push({ index, card });

    if (flippedCards.value.length === 2) {
      checkMatch();
    }
  };

  const checkMatch = () => {
    const [firstCard, secondCard] = flippedCards.value;

    if (firstCard.card.symbol === secondCard.card.symbol) {
      firstCard.card.matched = true;
      secondCard.card.matched = true;
    } else {
      setTimeout(() => {
        firstCard.card.flipped = false;
        secondCard.card.flipped = false;
      }, 1000);
    }

    flippedCards.value = [];
  };

  const resetGame = () => {
    const symbols = ['🍎', '🍌', '🍒', '🍇'];
    const shuffledCards = symbols.concat(symbols).map(symbol => ({
      symbol,
      flipped: false,
      matched: false,
    }));

    cards.value = shuffledCards.sort(() => 0.5 - Math.random());
    flippedCards.value = [];
  };

  resetGame();
</script>

<template>
  <div id="app">
    <h1>Memory Game</h1>
    <div class="memory-game">
      <div
        v-for="(card, index) in cards"
        :key="index"
        :class="['memory-card', { 'flipped': card.flipped || card.matched }]"
        @click="flipCard(index)"
      >
        <div class="front">{{ card.flipped || card.matched ? card.symbol : '?' }}</div>
      </div>
    </div>
    <button @click="resetGame">Reset Game</button>
  </div>
</template>

<style scoped>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    text-align: center;
    margin-top: 60px;
  }
  
  .memory-game {
    display: grid;
    grid-template-columns: repeat(4, 100px);
    grid-gap: 10px;
    justify-content: center;
  }

  .memory-card {
    width: 100px;
    height: 100px;
    background: #2d3748;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    border-radius: 10px;
    cursor: pointer;
    transition: transform 0.3s;
  }

  .memory-card.flipped, .memory-card.matched {
    background: #38a169;
    transform: rotateY(180deg);
  }

  button {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 1rem;
    cursor: pointer;
  }
</style>
