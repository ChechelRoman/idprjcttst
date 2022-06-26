<script setup>
import { onMounted, ref } from 'vue';
import AppForm from '../components/AppForm.vue';
import ItemCard from '../components/ItemCard.vue';
import AppPreloader from '../components/AppPreloader.vue';
import FadeTransition from '../components/FadeTransition.vue';
import AppSelect from '../components/AppSelect.vue';
import sortBy from 'lodash/sortBy';

const items = ref(JSON.parse(localStorage.getItem('items')) || []);

const filteredItems = ref([]);

const isDataLoaded = ref(false);

const activeFilter = ref('');

onMounted(() => {
  filteredItems.value = items.value;
  setTimeout(() => (isDataLoaded.value = true), 150);
});

const addItem = (itemData) => {
  const formattedObject = { ...itemData };
  formattedObject.price = Number(formattedObject.price);
  formattedObject.id = Date.now();
  items.value.push(formattedObject);
  localStorage.setItem('items', JSON.stringify(items.value));
  filterItems(activeFilter.value);
};

const deleteItem = (id) => {
  items.value = items.value.filter((item) => item.id !== id);
  localStorage.setItem('items', JSON.stringify(items.value));
  filterItems(activeFilter.value);
};

const selectOptions = [
  { label: 'По убыванию цены', value: 'priceDown' },
  { label: 'По возрастанию цены', value: 'priceUp' },
  { label: 'По названию', value: 'title' },
];

const filterItems = (filter) => {
  activeFilter.value = filter;
  switch (filter) {
    case '':
      filteredItems.value = items.value;
      break;
    case 'priceDown':
      filteredItems.value = sortBy(items.value, ['price']).reverse();
      break;
    case 'priceUp':
      filteredItems.value = sortBy(items.value, ['price']);
      break;
    case 'title':
      filteredItems.value = sortBy(items.value, ['title']);
      break;
  }
};
</script>

<template>
  <FadeTransition>
    <div v-if="isDataLoaded" class="container">
      <header class="header">
        <h1 class="heading">Добавление товара</h1>
        <AppSelect :options="selectOptions" @filter="filterItems" />
      </header>

      <section s class="content">
        <section class="form_container">
          <AppForm @submitData="addItem" />
        </section>
        <FadeTransition mode="out-in">
          <section v-if="items.length > 0" class="items_container">
            <transition-group name="list">
              <ItemCard
                v-for="item in filteredItems"
                :key="item.id"
                :url="item.url"
                :title="item.title"
                :description="item.description"
                :price="item.price"
                :id="item.id"
                @deleteItem="deleteItem"
              />
            </transition-group>
          </section>
          <p v-else class="empty_message">Список товаров пуст</p>
        </FadeTransition>
      </section>
    </div>
    <AppPreloader v-else :size="'60px'" />
  </FadeTransition>
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
    column-gap: 1rem;
    row-gap: 1rem;
    flex-wrap: wrap;
  }

  .empty_message {
    @include header();
    align-self: center;
    margin-inline: auto;
  }
}

.list-enter-active {
  animation: bounce-in 0.5s;
}
.list-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}
</style>
