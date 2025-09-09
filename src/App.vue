<template>
  <div class="container">
    <AppHeader :points="points" />
    <main class="main">
      <ul class="item-card-list">
        <ItemCard
          v-for="item in data"
          :key="item.id"
          v-bind="item"
          @flip-word="flipWord"
        />
      </ul>

      <AppButton @click="getData">{{
        isGameStarted ? "Начать заново" : "Начать игру"
      }}</AppButton>
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

const data = ref();
const isGameStarted = ref(false);

const getData = async () => {
  try {
    const response = await fetch("http://localhost:8080/api/random-words");
    if (!response.ok) {
      throw new Error("Failed to fetch data");
    }
    data.value = await response.json();
    data.value = data.value.map((item) => ({
      ...item,
      state: "closed",
      status: "pending",
    }));
    isGameStarted.value = true;
  } catch (error) {
    console.error(error);
  }
};

const flipWord = (state, word) => {
  data.value = data.value.map((item) => (item.word === word ? { ...item, state } : item));
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
  margin-bottom: 100px;
  counter-reset: item-card;
}
</style>
