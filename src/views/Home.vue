<template>
  <div class="home">
    <List />
  </div>
</template>

<script>
// @ is an alias to /src
import List from "@/components/List.vue";

export default {
  name: "Home",
  components: {
    List
  }
};
</script>
