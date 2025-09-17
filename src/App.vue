<template>
  <DefaultLayout>
    <ProductGrid/>
  </DefaultLayout>
</template>

<script lang="ts">
import DefaultLayout from "./layouts/DefaultLayout.vue";
import ProductGrid from "./components/ProductGrid.vue";

export default {
  components: {ProductGrid, DefaultLayout}
}
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
