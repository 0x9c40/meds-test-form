<template>
  <div
    class="selector-option"
    :class="{ 'selector-option--selected': is_selected }"
    @click="toggle_selection"
  >
    {{ option }}
  </div>
</template>

<script>
export default {
  name: "SelectorOption",

  props: {
    option: {
      type: String,
      default: "",
    },
    isSelectorMultiple: {
      type: Boolean,
      default: false,
    },
    selectedOptions: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      is_selected: false,
    };
  },

  methods: {
    toggle_selection() {
      if (this.isSelectorMultiple) {
        if (this.is_selected) {
          this.$emit("deselect", this.option);
        } else {
          this.$emit("select", this.option);
        }
        this.is_selected = !this.is_selected;
      } else {
        if (this.is_selected) {
          this.$emit("deselect", this.option);
          this.is_selected = !this.is_selected;
        } else {
          if (this.selectedOptions.length === 0) {
            this.$emit("select", this.option);
            this.is_selected = !this.is_selected;
          }
        }
      }
    },
  },
};
</script>

<style lang="scss">
.selector-option {
  margin-bottom: 2px;
  padding: 10px;
  border: 1px solid #e8e8e8;
  transition: border 0.1s ease;
  // border-radius: 5px;

  &--selected {
    background-color: darken(#e8e8e8, 0.2);
  }

  &:last-child {
    border-radius: 0px 0px 5px 5px;
  }

  &:hover {
    border-color: #cfcfcf;
  }
}
</style>