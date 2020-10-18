<template>
  <form class="form">
    <AttributesFormSection />
  </form>
</template>

<script>
import AttributesFormSection from "./sections/Attributes.vue";

export default {
  name: "ClientForm",

  components: {
    AttributesFormSection,
  },
};
</script>

<style lang="scss">
</style>