<template>
  <div class="surah-detail">
    <div class="container text-center my-5">
      <h3>Surat {{ surah.id }}</h3>
    </div>
    <div class="container">
      <ul class="list-unstyled mt-5">
        <li class="media" v-for="(ayat, index) in ayat" :key="index">
          <hr />
          <p class="badge badge-secondary text-wrap p-2">
            {{ ayat.number.inSurah }}
          </p>
          <div class="media-body mb-4">
            <h3 class="text-right">{{ ayat.text.arab }}</h3>
            <audio controls>
              <source :src="ayat.audio.primary" type="audio/mpeg" />
            </audio>
            <p>
              <strong> {{ ayat.text.transliteration.en }} </strong>
            </p>
            <quote class="text-muted font-italic">{{
              ayat.translation.id
            }}</quote>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import config from "../util/config.js";

export default {
  data() {
    return {
      id: this.$route.params.id,
      surah: {},
      ayat: null,
      prebismillah: {}
    };
  },
  created() {
    axios
      .get(`${config.baseUrl}/surah/` + this.id)
      .then(response => {
        this.surah = response.data.data.name.transliteration;
        this.ayat = response.data.data.verses;
        this.prebismillah = response.data.data.preBismillah.text;
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
