<template>
  <div id="app">
    <NavBar></NavBar>
    <AppForm></AppForm>
    <AppFooter></AppFooter>
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import AppForm from "./components/AppForm.vue";
import AppFooter from "./components/AppFooter.vue";

// Vue Instance
export default {
  components: {
    NavBar,
    AppForm,
    AppFooter,
  },
};
</script>

<style lang="scss">
@import "./assets/styles.scss";
@import "./assets/variables.scss";
</style>
