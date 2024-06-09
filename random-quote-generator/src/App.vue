<script setup>
import QuoteCard from './components/QuoteCard.vue';
</script>

<template>
  <div class="quote-card-wrapper">
    <QuoteCard />
  </div>
</template>

<style scoped>
.quote-card-wrapper{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
