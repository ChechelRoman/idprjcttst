<script setup>
const emit = defineEmits(['click']);
</script>

<template>
  <button v-bind="$attrs" class="button" @click="emit('click')">
    <slot></slot>
  </button>
</template>

<style lang="scss" scoped>
@use '@/assets/styles/abstracts' as *;

.button {
  @include button();
}
</style>
