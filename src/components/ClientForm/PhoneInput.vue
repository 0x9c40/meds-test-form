<template>
  <FormInput
    :label="label"
    :name="name"
    :error="error"
    :value="value"
    @input="$emit('input', $event)"
  >
    <slot></slot>
  </FormInput>
</template>

<script>
import FormInput from "./FormInput.vue";

export default {
  name: "PhoneInput",

  components: {
    FormInput,
  },

  props: {
    label: {
      default: "",
      type: String,
    },
    error: {
      default: false,
      type: Boolean,
    },
    value: {
      default: "",
      type: String,
    },
    name: {
      default: "",
      type: String,
    },
  },

  watch: {
    value() {
      this.$nextTick(this.clean_input);
    },
  },

  methods: {
    clean_input() {
      this.$emit("input", this.value.replace(/\D/g, "").slice(0, 11));
    },
  },
};
</script>

<style lang="scss">
</style>