<template>
  <div>
    <div class="loading" v-if="loading">Loading.....</div>
    <div class="list" v-else>
      <ul>
        <li v-for="(surah, index) in surah" :key="index">
          <router-link v-bind:to="'/surah/' + surah.number">{{
            surah.name.translation.id
          }}</router-link>
        </li>
      </ul>
    </div>
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
      loading: true,
      surah: null
    };
  },
  mounted() {
    axios
      .get(url)
      .then(response => {
        this.surah = response.data.data;
      })
      .catch(error => {
        console.log(error);
      })
      .finally(() => (this.loading = false));
  }
};
</script>
