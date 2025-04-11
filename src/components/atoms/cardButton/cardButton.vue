<template>
    <div class="card-button">
      <img :src="icon_card" @click="handleChange" />

    </div>
</template>

<script setup>
import icon_card from '../../../assets/icon_card.svg'
let card = true;

const handleChange = () => {
  card = !card
  localStorage.setItem('card', JSON.stringify(card));
  window.dispatchEvent(new Event('storage'));
};
</script>

<style lang="scss" scoped>
  @import "./index.scss";
</style>