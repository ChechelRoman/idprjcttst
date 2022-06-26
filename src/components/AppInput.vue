<script setup>
import { useField } from 'vee-validate';

const props = defineProps(['id', 'placeholder', 'label', 'required', 'type']);

const isRequired = (inputValue) => {
  if (inputValue && inputValue.trim()) {
    return true;
  }
  return 'Поле является обязательным';
};

const { value, errorMessage } = useField(`${props.id}`, props.required ? isRequired : undefined);
</script>

<template>
  <div class="form_field">
    <label class="form_field__label" :for="props.id"
      >{{ props.label }}<span class="dot" v-if="props.required"></span
    ></label>
    <input
      v-if="props.type === 'input'"
      v-model="value"
      class="form_field__input"
      type="text"
      :id="props.id"
      :placeholder="props.placeholder"
    />
    <textarea
      v-else
      v-model="value"
      class="form_field__textarea"
      :id="props.id"
      :placeholder="props.placeholder"
    ></textarea>
    <span class="form_field__error">{{ errorMessage }}</span>
  </div>
</template>

<style scoped lang="scss">
@use '@/assets/styles/abstracts' as *;

.form_field {
  display: flex;
  flex-direction: column;
  row-gap: 0.25rem;

  &__label {
    @include inputLabel();

    .dot {
      position: relative;

      &::before {
        content: '';
        height: 0.25rem;
        width: 0.25rem;
        display: inline-block;
        position: absolute;
        top: 0;
        border-radius: 50%;
        background-color: $ui-primary-red;
      }
    }
  }

  &__input {
    @include input();
  }

  &__textarea {
    @include textarea();
  }

  &__error {
    @include errorText();
    height: 0.675rem;
  }
}
</style>
