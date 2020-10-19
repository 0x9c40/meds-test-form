<template>
  <form class="form">
    <AttributesFormSection :touch="touch" />
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
      touch: 0,
    };
  },

  methods: {
    createUser() {
      this.touch++;
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