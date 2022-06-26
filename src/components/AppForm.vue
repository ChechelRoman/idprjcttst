<script setup>
import AppInput from './AppInput.vue';
import AppButton from './AppButton.vue';
import { useForm } from 'vee-validate';
import { ref } from 'vue';

const emit = defineEmits(['sumbit']);

const { handleSubmit, meta, resetForm } = useForm();

const isDataSubmitted = ref(false);

const onSubmit = handleSubmit((values) => {
  emit('sumbit', values);
  isDataSubmitted.value = true;
  setTimeout(() => (isDataSubmitted.value = false), 2000);
  resetForm();
});
</script>

<template>
  <form class="form" @submit="onSubmit">
    <div class="form_wrapper">
      <AppInput
        id="name"
        placeholder="Введите наименование товара"
        label="Наименование товара"
        :required="true"
        type="input"
      />
      <AppInput id="description" placeholder="Введите описание товара" label="Описание товара" :required="false" />
      <AppInput
        id="url"
        placeholder="Введите ссылку"
        label="Ссылка на изображение товара"
        :required="true"
        type="input"
      />
      <AppInput id="price" placeholder="Введите цену" label="Цена товара" :required="true" type="input" />
    </div>
    <AppButton type="submit" :disabled="!meta.valid">Добавить</AppButton>
    <transition name="fade">
      <p v-if="isDataSubmitted" class="success_message">Товар успешно добавлен</p>
    </transition>
  </form>
</template>

<style lang="scss" scoped>
@use '@/assets/styles/abstracts' as *;

.form_wrapper {
  display: flex;
  flex-direction: column;
  row-gap: 0.125rem;
  margin-bottom: 0.625rem;
}

.success_message {
  @include buttonText();
  margin-top: 0.5rem;
  text-align: center;
  color: $ui-primary-green;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 300ms ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
