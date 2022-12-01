<template>
  <div id="app">
    <header-navbar />
    <router-view />
  </div>
</template>

<script>
import HeaderNavbar from "./components/HeaderNavbar.vue";
export default {
  components: {
    HeaderNavbar,
  },
};
</script>

<style></style>
