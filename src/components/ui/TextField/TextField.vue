<script setup lang="ts">
import Typography from '@/components/ui/Typography'

import type { TextFieldProps } from './TextField.interface'

withDefaults(defineProps<TextFieldProps>(), {
  type: 'text'
})

const model = defineModel({
  required: false
})
</script>

<template>
  <label
    :class="[
      'field',
      {
        field_error: isError,
        field_readonly: isReadonly
      }
    ]"
  >
    <Typography v-if="isError" type="p-2" class="field__error">{{ errorMessage }}</Typography>

    <div class="field__content">
      <Typography class="field__caption" type="p-3">{{ label }}</Typography>

      <input
        class="field__input"
        v-model="model"
        :name="name"
        :type="type"
        :placeholder="placeholder"
        :readonly="isReadonly"
      />
    </div>
  </label>
</template>

<style scoped lang="scss">
.field {
  width: 100%;

  &__error {
    color: #db524e; // COLORS
  }

  &__content {
    user-select: none;
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 2px;
    padding: 8px 15px;
    background-color: #ffffff; // COLORS
    border: 1px solid #f1f1f1; // COLORS
    border-radius: 5px;
  }

  &__caption {
    color: #11111148; // COLORS
  }

  &__input {
    font-size: var(--typography-p-2);
    color: #000000; // COLORS
    background: none;
    outline: none;
    border: none;

    // Disable number input arrows
    &[type='number'] {
      -moz-appearance: textfield;
      &::-webkit-outer-spin-button,
      &::-webkit-inner-spin-button {
        -webkit-appearance: none;
      }
    }

    &::placeholder {
      color: #11111148; // COLORS
    }
  }

  &_readonly {
    cursor: default;

    .field__input {
      cursor: default;
    }
  }

  &_error {
    .field__content {
      background-color: #f9e3e3; // COLORS
    }
  }
}
</style>
