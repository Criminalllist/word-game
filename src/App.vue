<template>
  <div class="container">
    <header v-if="false" class="header">
      <h1 class="header__title">ЗАПОМНИ СЛОВО</h1>
      <div class="header__counter life-counter">
        <div class="life-counter__item">100</div>
      </div>
    </header>
    <main class="main">
      <AppButton />
    </main>
  </div>
</template>

<script setup>
import AppButton from "@/common/components/AppButton.vue";
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px;
}
</style>
