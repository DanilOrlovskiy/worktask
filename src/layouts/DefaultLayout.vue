<template>
  <div class="min-h-screen flex flex-col">
    <AppHeader/>
    <main class="content flex-1">
      <slot/>
    </main>
    <AppFooter/>
  </div>
</template>

<script lang="ts">
import AppHeader from "../components/AppHeader.vue";
import AppFooter from "../components/AppFooter.vue";

export default {
  components: {AppFooter, AppHeader}
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
