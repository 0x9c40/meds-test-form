<template>
  <form class="form">
    <AttributesFormSection :is-form-dirty="dirty" />
    <div class="mandatory-field-tip">* - обязательное поле</div>
    <input type="button" value="Создать" @click="createUser" />
  </form>
</template>

<script>
import AttributesFormSection from "./sections/Attributes.vue";

export default {
  name: "ClientForm",

  components: {
    AttributesFormSection,
  },

  data() {
    return {
      dirty: false,
    };
  },

  methods: {
    createUser() {
      this.dirty = true;
    },
  },
};
</script>

<style lang="scss">
.mandatory-field-tip {
  font-family: "Roboto", sans-serif;
  color: #374853;
  font-size: 12px;
}
</style>