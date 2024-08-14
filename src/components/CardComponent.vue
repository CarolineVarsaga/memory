<!-- <script setup lang="ts">
  import { ICard } from '../interface/icard.ts';  

  const props = defineProps<{ card: ICard, index: number }>();
  const emit = defineEmits<{ (e: 'flip', index: number): void }>();

  const flipCard = () => {
    emit('flip', props.index);
  };
</script>

<template>
  <div
    :class="['memory-card', { 'flipped': card.flipped || card.matched }]"
    @click="flipCard"
  >
    <div class="front">({ card.flipped || card.matched ? card.symbol : '?' })</div>
  </div>
</template>

<style scoped>
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
</style> -->