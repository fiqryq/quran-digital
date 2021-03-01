<template>
  <div class="surah-detail">
    <h1>Surat {{ surah.id }}</h1>
    <!-- Perulangan -->

    <div class="content" v-for="(ayat, index) in ayat" :key="index">
      <p>{{ ayat.number.inSurah }}</p>
      <p>{{ ayat.text.arab }}</p>
      <p>{{ ayat.text.transliteration.en }}</p>
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
