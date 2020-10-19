<template>
  <div class="form-checkbox">
    <input
      :name="name"
      class="form-checkbox__checkbox"
      type="checkbox"
      @change="$emit('input', $event.target.checked)"
    />
    <div class="form-checkbox__label">{{ label }}</div>
  </div>
</template>

<script>
export default {
  name: "FormCheckbox",

  props: {
    name: {
      type: String,
      default: "",
    },
    label: {
      type: String,
      default: "",
    },
  },
};
</script>

<style lang="scss">
.form-checkbox {
  display: flex;
  height: 30px;
  align-items: center;

  &__checkbox {
    margin-right: 8px;
  }

  &__label {
    font-family: "Roboto", sans-serif;
  }
}
</style>