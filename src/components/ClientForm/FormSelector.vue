<template>
  <div :name="name" class="form-selector">
    <div
      class="form-selector__label"
      :class="{ 'form-selector__label--opened': isSelectorOpened }"
      @click="isSelectorOpened = !isSelectorOpened"
    >
      {{ label }}
    </div>
    <SelectedOptions
      :options="selectedOptions"
      @click.native="isSelectorOpened = !isSelectorOpened"
    />
    <div v-show="isSelectorOpened" class="form-selector-options">
      <SelectorOption
        v-for="option in options"
        :key="option"
        :option="option"
        :selected-options="selectedOptions"
        :is-selector-multiple="multiple"
        class="form-selector-options__option"
        @deselect="deselect"
        @select="select"
      />
    </div>
  </div>
</template>

<script>
import SelectorOption from "./SelectorOption.vue";
import SelectedOptions from "./SelectedOptions.vue";

export default {
  name: "FormSelector",

  components: {
    SelectorOption,
    SelectedOptions,
  },

  props: {
    options: {
      default: () => [],
      type: Array,
    },
    name: {
      default: "",
      type: String,
    },
    label: {
      default: "",
      type: String,
    },
    multiple: {
      default: false,
      type: Boolean,
    },
  },

  data() {
    return {
      isSelectorOpened: false,
      selectedOptions: [],
    };
  },

  methods: {
    deselect(option) {
      this.selectedOptions = this.selectedOptions.filter(
        (item) => item !== option
      );
    },
    select(option) {
      this.selectedOptions.push(option);
    },
  },
};
</script>

<style lang="scss">
.form-selector {
  margin-bottom: 16px;
  display: flex;
  flex-direction: column;
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  width: 100%;

  &__label {
    font-family: "Roboto", sans-serif;
    display: inline-block;
    margin-bottom: 4px;

    &--error {
      color: red;
    }
  }
}
</style>