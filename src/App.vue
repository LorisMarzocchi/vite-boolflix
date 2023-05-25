<script>
import AppHeader from "./components/AppHeader.vue";
import AppSearch from "./components/AppSearch.vue";
import AppMain from "./components/AppMain.vue";
import axios from "axios";
import { store } from "./store";

export default {
  data() {
    return {
      store,
    };
  },
  components: {
    AppHeader,
    AppMain,
    AppSearch,
  },
  methods: {

    requestDataFromApi() {
      axios
        .get('https://api.themoviedb.org/3/search/movie?query=', {
          params: {
            api_key: '95f92b62827d48d27c5483a9415a484d',
            query: this.store.value,
          }
        })
        .then(response => (this.store.cardList = response.data.results));
    },
    // requestDataTvSeries() {
    //   axios
    //     .get('https://api.themoviedb.org/3/search/tv?api_key=', {
    //       params: {
    //         api_key: '95f92b62827d48d27c5483a9415a484d',
    //         query: this.store.value,
    //       }
    //     })
    //     .then(response => (this.store.cardList = response.data.results));
    // },
  },
  created() {
    // qui fare la richiesta all'api

  },

}




</script>

<template>
  <AppHeader />
  <AppSearch @performSearch="requestDataFromApi" />
  <AppMain />
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
