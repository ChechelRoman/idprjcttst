<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps(['size']);

const styles = computed(() => {
  return {
    width: props.size,
    height: props.size,
  };
});
</script>

<template>
  <svg v-bind:style="styles" class="spinner spinner--circle" viewBox="0 0 66 66" xmlns="http://www.w3.org/2000/svg">
    <circle class="path" fill="none" stroke-width="6" stroke-linecap="round" cx="33" cy="33" r="30"></circle>
  </svg>
</template>

<style lang="scss" scoped>
@use '@/assets/styles/abstracts' as *;

$offset: 187;
$duration: 1.4s;
.spinner {
  animation: circle-rotator $duration linear infinite;
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);

  @media screen and (max-width: 700px) {
    left: 43%;
    top: 45%;
  }
  * {
    line-height: 0;
    box-sizing: border-box;
  }
}
@keyframes circle-rotator {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(270deg);
  }
}
.path {
  stroke-dasharray: $offset;
  stroke-dashoffset: 0;
  transform-origin: center;
  animation: circle-dash $duration ease-in-out infinite, circle-colors ($duration * 4) ease-in-out infinite;
}
@keyframes circle-colors {
  0% {
    stroke: $ui-primary-green;
  }
  25% {
    stroke: $ui-primary-red;
  }
  50% {
    stroke: $ui-primary-green;
  }
  75% {
    stroke: $ui-primary-red;
  }
  100% {
    stroke: $ui-primary-green;
  }
}
@keyframes circle-dash {
  0% {
    stroke-dashoffset: $offset;
  }
  50% {
    stroke-dashoffset: calc($offset / 4);
    transform: rotate(135deg);
  }
  100% {
    stroke-dashoffset: $offset;
    transform: rotate(450deg);
  }
}
</style>
