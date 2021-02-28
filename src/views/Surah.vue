<template>
  <div class="surah">
    <p>{{ datasurah }}</p>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);

const url = "https://api.quran.sutanlab.id/surah/";
export default {
  data() {
    return {
      id: this.$route.params.id,
      datasurah: {}
    };
  },
  created() {
    axios
      .get(url + this.id)
      .then(response => {
        this.datasurah = response.data.data;
      })
      .catch(error => {
        console.log(error);
      })
      .finally();
  }
};
</script>
