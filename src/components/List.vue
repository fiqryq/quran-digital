<template>
  <div>
    <!-- container searchbox -->
    <div class="container">
      <div class="row align-item-center justify-content-center">
        <form class="col-xl-12 col-md-12 col-lg-12 col-sm-12 col-12 p-1 mt-4">
          <input
            class="form-control form-control-lg mb-1 font-italic"
            type="text"
            v-model="search"
            placeholder="cari surat..."
          />
        </form>
      </div>
    </div>
    <!-- Container surah -->
    <div class="container mb-3">
      <div class="loading" v-if="loading">
        <div class="spinner-grow" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>
      <div class="content-surah" v-else>
        <div class="row">
          <div
            class="col-xl-4 col-sm-6 col-12 p-1"
            v-for="(surah, index) in filterSurah"
            :key="index"
          >
            <div class="card">
              <div class="card-content">
                <div class="card-body">
                  <div class="media d-flex">
                    <div class="media-body text-left">
                      <h3 class="surah-name">
                        <router-link v-bind:to="'/surah/' + surah.number">
                          {{ surah.name.transliteration.id }}
                        </router-link>
                      </h3>
                      <span class="text-muted">{{
                        surah.name.translation.id
                      }}</span>
                    </div>
                    <div class="align-self-center">
                      <h3 class="surah-name-arab">{{ surah.name.short }}</h3>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import config from "../util/config.js";

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
      .get(`${config.baseUrl}/surah`)
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
        return surah.name.transliteration.id
          .toLowerCase()
          .split("-")
          .join(" ")
          .match(this.search);
      });
    }
  }
};
</script>
<style scope>
.loading {
  width: 100%;
  max-width: 700px;
  margin: auto;
  align-items: center;
  height: 100vh;
  display: flex;
  justify-content: center;
}

.card {
  border: none;
}

.form-control {
  border: none;
}
/* Remove Underline Router link */
a {
  text-decoration: none;
}

a:hover {
  text-decoration: none;
}

/* Color title */
.surah-name a {
  color: rgb(0, 194, 32);
}

.surah-name a:hover {
  color: rgb(0, 148, 25);
}
</style>
