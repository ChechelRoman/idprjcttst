<script setup>
import MainView from './views/MainView.vue';
</script>

<template>
  <MainView />
</template>

<style lang="scss">
@use '@/assets/styles/base.scss';
@use '@/assets/styles/abstracts' as *;

#app {
  min-height: 100vh;
  background-color: $ui-layout;
}
</style>
