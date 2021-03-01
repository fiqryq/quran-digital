<template>
  <div>
    <div class="container">
      <input type="text" v-model="search" placeholder="cari surat" />
      <div class="loading" v-if="loading">
        <div class="spinner-grow" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>
      <div v-else>
        <div class="card-group">
          <div class="row">
            <div
              class="col-4"
              v-for="(surah, index) in filterSurah"
              :key="index"
            >
              <router-link v-bind:to="'/surah/' + surah.number">
                <div class="card mb-5">
                  <div class="card-body">
                    <div class="card-title">
                      {{ surah.name.transliteration.id }}
                    </div>
                  </div>
                </div>
              </router-link>
            </div>
          </div>
        </div>
      </div>
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
      surah: {},
      search: ""
    };
  },
  created() {
    axios
      .get(url)
      .then(response => {
        this.surah = response.data.data;
      })
      .catch(error => {
        console.log(error);
      })
      .finally(() => (this.loading = false));
  },
  computed: {
    filterSurah: function() {
      return this.surah.filter(surah => {
        return surah.name.transliteration.id.match(this.search);
      });
    }
  }
};
</script>
<style scope>
.card {
  max-width: 400px;
  width: 300px;
}
.loading {
  width: 100%;
  max-width: 700px;
  margin: auto;
  align-items: center;
  height: 100vh;
  display: flex;
  justify-content: center;
}
</style>
