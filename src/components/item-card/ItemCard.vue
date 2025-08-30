<template>
  <li class="item-card" @click="flipWord(), changeStatus()">
    <div class="item-card__inner">
      <span class="item-card__word">{{ word }}</span>
      <div class="item-card__bottom">
        <div class="item-card__status">
          <span class="item-card__status-text" v-if="status">{{
            status ? "Перевернуть" : "Завершено"
          }}</span>
          <template v-else>
            <span class="item-card__status-icon item-card__status-icon--error">
              <AppIcon
                name="error"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="#D00303"
              />
            </span>
            <span class="item-card__status-icon item-card__status-icon--success">
              <AppIcon
                name="success"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="#09BB00"
              />
            </span>
          </template>
        </div>
      </div>

      <div v-if="!status" class="item-card__result">
        <span
          v-if="word !== 'Привет'"
          class="item-card__result-icon item-card__result-icon--error"
        >
          <AppIcon
            name="error"
            width="36"
            height="36"
            viewBox="0 0 36 36"
            fill="#D00303"
          />
        </span>
        <span
          v-if="word == 'Привет'"
          class="item-card__result-icon item-card__result-icon--success"
        >
          <AppIcon
            name="success"
            width="36"
            height="36"
            viewBox="0 0 36 36"
            fill="#09BB00"
          />
        </span>
      </div>
    </div>
  </li>
</template>

<script setup>
import AppIcon from "@/common/components/AppIcon.vue";

const props = defineProps({
  word: {
    type: String,
    required: true,
  },
  status: {
    type: Boolean,
    required: true,
  },
});

const emit = defineEmits(["changeStatus", "flipWord"]);

const changeStatus = () => {
  emit("changeStatus", !props.status);
};

const flipWord = () => {
  emit("flipWord");
};
</script>

<style lang="scss" scoped>
.item-card {
  max-width: 250px;
  width: 100%;
  min-height: 370px;
  padding: $space-l $space-main;
  background-color: $color-bg-card;
  border-radius: $border-radius-basic;
  box-shadow: $box-shadow-basic;
  counter-reset: item-card;
  cursor: pointer;
  user-select: none;

  &__inner {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    border-radius: $border-radius-small;
    border: $border-basic;

    &::before {
      content: counter(item-card, decimal-leading-zero);
      counter-increment: item-card;
      position: absolute;
      top: -7px;
      left: 15px;
      background-color: $color-bg-card;
    }
  }

  &__word {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-grow: 1;
    font-size: $font-size-m;
    color: $color-text-main;
  }

  &__bottom {
    position: relative;
    bottom: -15px;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 30px;
    background-color: $color-bg-card;
    flex-shrink: 0;
    z-index: 2;

    &::before {
      content: "";
      position: absolute;
      left: -6px;
      z-index: -1;
      width: calc(100% + 12px);
      height: 100%;

      background-color: $color-bg-card;
    }
  }

  &__status {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: $space-main;
    width: 100%;
    font-size: $font-size-s;
    font-weight: $font-weight-bold;
    text-transform: uppercase;

    &-icon {
      &--error {
        color: #d00303;
      }
      &--success {
        color: #09bb00;
      }
    }
  }

  &__result {
    position: absolute;
    top: -16px;
    left: 50%;
    translate: -50% 0;

    &-icon {
      &--error {
        color: #d00303;
      }
      &--success {
        color: #09bb00;
      }
    }
  }
}
</style>
