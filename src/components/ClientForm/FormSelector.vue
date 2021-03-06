<template>
  <div :name="name" class="form-selector">
    <div
      class="form-selector__label"
      :class="{ 'form-selector__label--error': error }"
      @click="toggleOptionsList"
    >
      {{ label }}
    </div>
    <SelectedOptions
      :options="selectedOptions"
      :error="error"
      @click.native="toggleOptionsList"
    />
    <div class="form-selector-options-wrapper">
      <div v-show="isSelectorOpened" class="form-selector-options">
        <div
          v-for="option in options"
          :key="option"
          class="selector-option"
          :class="{
            'selector-option--selected': selectedOptions.includes(option),
          }"
          @click="toggleSelectionFor(option)"
        >
          {{ option }}
        </div>
      </div>
    </div>
    <div class="form-selector-error">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import SelectedOptions from "./SelectedOptions.vue";

export default {
  name: "FormSelector",

  components: {
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
    error: {
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
    toggleOptionsList() {
      this.isSelectorOpened = !this.isSelectorOpened;
    },

    isSelected(option) {
      return this.selectedOptions.includes(option);
    },

    select(option) {
      this.selectedOptions.push(option);
    },

    deselect(option) {
      this.selectedOptions = this.selectedOptions.filter(
        (item) => item !== option
      );
    },

    emptySelectedOptions() {
      this.selectedOptions = [];
    },

    toggleSelectionFor(option) {
      if (this.isSelected(option)) {
        this.deselect(option);
      } else {
        if (!this.multiple) {
          this.emptySelectedOptions();
          this.toggleOptionsList();
        }
        this.select(option);
      }

      if (this.multiple) {
        this.$emit("input", this.selectedOptions);
      } else {
        this.$emit("input", ...this.selectedOptions);
      }
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

.form-selector-options-wrapper {
  position: relative;
}

.form-selector-options {
  position: absolute;
  width: 100%;
  top: 0;
  z-index: 1;
}

.selector-option {
  margin: 3px 0px;
  padding: 10px;
  border: 1px solid #e8e8e8;
  transition: border 0.1s ease;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
  background-color: #fff;

  &--selected {
    background-color: darken(#e8e8e8, 0.2);
    box-shadow: none;
  }

  &:last-child {
    border-radius: 0px 0px 5px 5px;
  }

  &:hover {
    border-color: #cfcfcf;
  }
}

.form-selector-error {
  font-family: "Roboto", sans-serif;
  color: red;
  font-size: 12px;
  margin-top: 2px;
}
</style>