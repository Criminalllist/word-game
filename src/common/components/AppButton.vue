<template>
  <button class="button" type="button">
    <slot>Начать игру</slot>
  </button>
</template>

<script setup></script>

<style lang="scss" scoped>
@use '@/assets/scss/variables.scss' as vars;

.button {
  display: grid;
  place-items: center;

  min-width: 315px;
  padding: 16px 10px;
  border-radius: 100px;
  border: none;

  background-color: vars.$color-dark-blue;
  font-size: vars.$font-size-large;
  color: vars.$color-text-white;
  font-weight: vars.$font-weight-regular;
}
</style>
