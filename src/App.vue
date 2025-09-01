<template>
  <div class="container">
    <AppHeader :points="points" />
    <main class="main">
      <ul class="item-card-list">
        <ItemCard v-bind="data" @flip-word="flipWord" />
      </ul>

      <AppButton />
    </main>
  </div>

  <SpritesLoader />
</template>

<script setup>
import { ref } from "vue";

import AppButton from "@/common/components/AppButton.vue";
import SpritesLoader from "@/common/components/SpritesLoader.vue";
import AppHeader from "@/components/header/AppHeader.vue";
import ItemCard from "@/components/item-card/ItemCard.vue";

const points = ref(100);

const data = ref({
  word: "Hello",
  translation: "Привет",
  state: "closed",
  status: "pending",
});

const flipWord = (state) => {
  data.value.state = state;
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
}

main {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.item-card-list {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: $space-l;
}
</style>
