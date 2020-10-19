<template>
  <div class="form-date-picker">
    <label
      class="form-date-picker__label"
      :class="{ 'form-date-picker__label--error': error }"
      :for="name"
      >{{ label }}</label
    >
    <input
      :id="name"
      type="date"
      :name="name"
      class="form-date-picker__input"
      :class="{ 'form-date-picker__input--error': error }"
      @input="$emit('input', $event.target.value)"
    />
    <div class="form-date-picker-error">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormDatePicker",

  props: {
    label: {
      default: "",
      type: String,
    },
    name: {
      default: "",
      type: String,
    },
    error: {
      default: false,
      type: Boolean,
    },
  },
};
</script>

<style lang="scss">
.form-date-picker {
  margin-bottom: 10px;

  &__label {
    font-family: "Roboto", sans-serif;
    display: inline-block;
    margin-bottom: 2px;

    &--error {
      color: red;
    }
  }

  &__input {
    font-family: "Roboto", sans-serif;
    color: #374853;
    border: 1px solid #e8e8e8;
    border-radius: 5px;
    width: 100%;
    height: 32px;
    padding: 0 10px;
    font-size: 16px;
    transition: border 0.1s ease;

    &--error {
      border-color: red;
    }

    &:hover {
      border-color: #cfcfcf;
    }

    &:focus {
      border-color: #a8a8a8;
      outline: none;
    }
  }
}
.form-date-picker-error {
  font-family: "Roboto", sans-serif;
  color: red;
  font-size: 12px;
  margin-top: 2px;
}
</style>