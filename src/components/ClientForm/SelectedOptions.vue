<template>
  <div class="selected-options" :class="{ 'selected-options--error': error }">
    <span v-if="options.length === 0">-- Не выбрано --</span>
    <span
      v-for="option in options"
      :key="option"
      class="selected-options__option"
      >{{ option }}</span
    >
  </div>
</template>

<script>
export default {
  name: "SelectedOptions",

  props: {
    options: {
      type: Array,
      default: () => [],
    },
    error: {
      default: false,
      type: Boolean,
    },
  },
};
</script>

<style lang="scss">
.selected-options {
  font-family: "Roboto", sans-serif;
  color: #374853;
  border: 1px solid #e8e8e8;
  border-radius: 5px;
  width: 100%;
  height: 36px;
  padding: 0 10px;
  font-size: 16px;
  transition: border 0.1s ease;
  display: flex;
  align-items: center;

  &:hover {
    border-color: #cfcfcf;
  }

  &--error {
    border-color: red;
  }

  &__option {
    &:not(:last-child) {
      &:after {
        content: ",\00a0";
      }
    }
  }
}
</style>