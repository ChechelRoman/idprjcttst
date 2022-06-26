<script setup>
import { ref } from 'vue';
import { onClickOutside } from '@vueuse/core';
import IconSelectArrow from './icons/IconSelectArrow.vue';

const props = defineProps(['options']);

const emit = defineEmits(['filter']);

const isSelectOpen = ref(false);

const optionsContainer = ref(null);

onClickOutside(optionsContainer, () => (isSelectOpen.value = false));

const selectedText = ref('По умолчанию');

const handleOptionClick = (option) => {
  selectedText.value = option.label;
  emit('filter', option.value);
  isSelectOpen.value = false;
};
</script>

<template>
  <div class="select_container">
    <div class="select_closed" @click="isSelectOpen = true">
      <p class="select_option-selected">{{ selectedText }}</p>
      <IconSelectArrow class="select_arrow" />
    </div>
    <div v-if="isSelectOpen" class="options_container" ref="optionsContainer">
      <div v-for="(option, index) in props.options" :key="index" class="option" @click="handleOptionClick(option)">
        {{ option.label }}
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use '@/assets/styles/abstracts' as *;

.select_container {
  position: relative;
}

.select_closed {
  @include input;
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: $ui-primary-grey;
  column-gap: 0.3125rem;

  &:hover {
    cursor: pointer;
  }

  .select_arrow {
    color: $ui-primary-grey;
  }
}

.options_container {
  @include input();
  position: absolute;
  z-index: 10;
  top: 2.5rem;
  right: 0;
  padding: unset;
  display: flex;
  flex-direction: column;

  &:hover {
    border-color: transparent;
  }

  .option {
    cursor: pointer;
    padding: 0.5625rem 1rem;
    transition: all 200ms ease;

    &:hover {
      color: $ui-primary-white;
      background-color: $ui-primary-green;
    }
  }
}
</style>
