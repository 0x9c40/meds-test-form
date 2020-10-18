<template>
  <div>
    <ClientForm />
  </div>
</template>

<script>
import ClientForm from "./components/ClientForm/Form.vue";

export default {
  name: "App",

  components: {
    ClientForm,
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@100;300&display=swap");

* {
  box-sizing: border-box;
}

body {
  display: flex;
  justify-content: center;
}
</style>
