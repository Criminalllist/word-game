<template>
  <div class="life-points">
    <span class="life-points__score">{{ points ?? "-" }}</span>
    <span class="life-points__icon">
      <AppIcon name="life" width="24" height="24" viewBox="0 0 24 24" fill="#008BFE" />
    </span>
  </div>
</template>

<script setup>
import AppIcon from "@/common/components/AppIcon.vue";
defineProps({
  points: {
    type: Number,
    required: true,
  },
});
</script>

<style lang="scss" scoped>
.life-points {
  display: flex;
  align-items: center;
  gap: $space-xs;
  width: max-content;
  padding: $space-s $space-l;
  border-radius: 36px;
  background-color: $color-light-blue;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);

  &__score {
    font-weight: 700;
    color: $color-dark-blue;
  }

  &__icon {
    color: $color-dark-blue;
  }
}
</style>
