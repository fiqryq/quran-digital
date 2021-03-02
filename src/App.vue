<template>
  <div id="app">
    <router-view />
    <Footer class="mt-3" />
  </div>
</template>
<script>
import Footer from "@/components/Footer.vue";

export default {
  components: {
    Footer
  }
};
</script>
