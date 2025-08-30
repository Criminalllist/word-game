<template>
  <header class="header">
    <h1 class="header__title">Запомни слово</h1>
    <LifePoints :points="points" />
  </header>
</template>

<script setup>
import LifePoints from "@/components/life-points/LifePoints.vue";
defineProps({
  points: {
    type: Number,
    required: true,
  },
});
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: $space-l;
  padding-block: $space-xl;

  &__title {
    text-transform: uppercase;
    font-size: $font-size-large;
    font-weight: $font-weight-bold;
  }
}
</style>
