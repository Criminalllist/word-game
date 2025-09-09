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

      <p v-if="isLoading" class="loading-message">Загрузка...</p>

      <p v-if="isError" class="error-message">
        Не удалось загрузить данные, попробуйте еще раз
      </p>

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
const isError = ref(false);
const isLoading = ref(false);

const getData = async () => {
  try {
    isLoading.value = true;
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
    isError.value = false;
    isGameStarted.value = true;
    isLoading.value = false;
  } catch (error) {
    isError.value = true;
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

.loading-message {
  color: $color-text-primary;
  font-size: $font-size-m;
  font-weight: $font-weight-bold;
  text-align: center;
  margin-bottom: $space-xl;
}

.error-message {
  color: rgb(133, 17, 17);
  font-size: $font-size-m;
  font-weight: $font-weight-bold;
  text-align: center;
  margin-bottom: $space-xl;
}
</style>
