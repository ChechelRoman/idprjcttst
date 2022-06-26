<script setup>
const props = defineProps(['mode']);
</script>

<template>
  <transition name="fade" :mode="props.mode ? props.mode : 'default'">
    <slot></slot>
  </transition>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 300ms ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
