<script setup>
import AppForm from '../components/AppForm.vue';
import ItemCard from '../components/ItemCard.vue';
</script>

<template>
  <div class="container">
    <header class="header">
      <h1 class="heading">Добавление товара</h1>
    </header>
    <section class="content">
      <section class="form_container">
        <AppForm />
      </section>
      <section class="items_container"></section>
    </section>
  </div>
</template>

<style lang="scss">
@use '@/assets/styles/abstracts' as *;

.container {
  width: min(1440px, 90%);
  margin: 0 auto;
  padding: 2rem;
}

.header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;

  .heading {
    @include header();
  }
}

.content {
  display: flex;
  column-gap: 1rem;

  .form_container {
    width: 20.75rem;
    padding: 1.5rem;
    background-color: $ui-card-background;
    box-shadow: $ui-card-shadow;
    border-radius: 0.25rem;
    align-self: flex-start;
  }

  .items_container {
    width: calc(100% - 21.75rem);
    display: flex;
    justify-content: space-between;
    column-gap: 1rem;
    row-gap: 1rem;
    flex-wrap: wrap;
  }
}
</style>
