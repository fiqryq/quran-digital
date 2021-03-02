<template>
  <div class="surah-detail">
    <div class="container py-4 text-center">
      <h3>Surat {{ surah.id }}</h3>
    </div>
    <div class="container">
      <ul class="list-unstyled mt-4">
        <li class="media" v-for="(ayat, index) in ayat" :key="index">
          <hr />
          <p class="badge badge-secondary text-wrap p-2">
            {{ ayat.number.inSurah }}
          </p>
          <div class="media-body mb-3">
            <h3 class="text-right">{{ ayat.text.arab }}</h3>
            <p class="ml-2">{{ ayat.text.transliteration.en }}</p>
          </div>
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
      id: this.$route.params.id,
      surah: {},
      ayat: null
    };
  },
  created() {
    axios
      .get(url + this.id)
      .then(response => {
        this.surah = response.data.data.name.transliteration;
        this.ayat = response.data.data.verses;
      })
      .catch(error => {
        console.log(error);
      })
      .finally();
  }
};
</script>
<style scoped>
.container {
  max-width: 800px;
}
</style>
