<script setup>
import AppInput from './AppInput.vue';
import AppButton from './AppButton.vue';
import FadeTransition from './FadeTransition.vue';
import { useForm } from 'vee-validate';
import { ref } from 'vue';

const emit = defineEmits(['submitData']);

const { handleSubmit, meta, resetForm } = useForm();

const isDataSubmitted = ref(false);

const onSubmit = handleSubmit((values) => {
  emit('submitData', values);
  isDataSubmitted.value = true;
  setTimeout(() => (isDataSubmitted.value = false), 2000);
  resetForm();
});
</script>

<template>
  <form class="form" @submit="onSubmit">
    <div class="form_wrapper">
      <AppInput
        id="title"
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
    <FadeTransition>
      <p class="success_message"><span v-if="isDataSubmitted">Товар успешно добавлен</span></p>
    </FadeTransition>
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
  height: 1rem;
  margin-top: 0.5rem;
  text-align: center;
  color: $ui-primary-green;
}
</style>
