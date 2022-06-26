<script setup>
import { ref } from 'vue';
import IconDelete from './icons/IconDelete.vue';
import FadeTransition from './FadeTransition.vue';

const props = defineProps(['url', 'title', 'description', 'price', 'id']);

const emit = defineEmits(['deleteItem']);

const isDeleteIconShown = ref(false);

const emitDeleteItem = () => emit('deleteItem', props.id);
</script>

<template>
  <div class="card" @mouseover="isDeleteIconShown = true" @mouseleave="isDeleteIconShown = false">
    <FadeTransition>
      <button class="delete_button" v-if="isDeleteIconShown" @click="emitDeleteItem">
        <IconDelete class="delete_icon" />
      </button>
    </FadeTransition>
    <img class="card__image" :src="`${props.url}`" alt="item image" />
    <h3 class="card__title">{{ props.title }}</h3>
    <p class="card__description">{{ props.description ? props.description : 'Нет описания' }}</p>
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
  position: relative;

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
    min-width: 0;
    text-overflow: ellipsis;
    overflow: hidden;
    margin-bottom: 1rem;
    padding: 0 1rem;
  }

  &__price {
    @include cardPrice();
    margin-top: auto;
    padding: 0 1rem;
    padding-bottom: 1.5rem;
  }
}

.delete_button {
  position: absolute;
  top: -0.5rem;
  right: -0.5rem;

  .delete_icon {
    color: $ui-primary-red;
    transition: all 200ms ease-in-out;
    cursor: pointer;

    &:hover {
      color: #f85f5f;
    }
  }
}
</style>
