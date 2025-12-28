<template>
  <ProductDisplay />
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";
import "./assets/style/page.css";

export default {
  name: "App",
  components: {
    ProductDisplay,
  },
};
</script>

<style>
/* Global styles are imported from page.css */
</style>
