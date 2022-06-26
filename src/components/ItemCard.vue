<script setup>
const props = defineProps(['url', 'title', 'description', 'price']);
</script>

<template>
  <div class="card">
    <img class="card__image" :src="`${props.url}`" alt="item image" />
    <h3 class="card__title">{{ props.title }}</h3>
    <p class="card__description">{{ props.description }}</p>
    <p class="card__price">{{ props.price }} руб.</p>
  </div>
</template>

<style lang="scss" scoped>
@use '@/assets/styles/abstracts' as *;

.card {
  display: flex;
  flex-direction: column;
  width: 20.75rem;
  row-gap: 1rem;
  background-color: $ui-card-background;
  box-shadow: $ui-card-shadow;
  border-radius: 0 0 0.25rem 0.25rem;

  &__image {
    height: 12.5rem;
    border-radius: 0.25rem 0.25rem 0 0;
  }

  &__title {
    @include cardTitle();
    padding: 0 1rem;
  }

  &__description {
    @include cardDescription();
    margin-bottom: 1rem;
    padding: 0 1rem;
  }

  &__price {
    @include cardPrice();
    padding: 0 1rem;
    padding-bottom: 1.5rem;
  }
}
</style>
