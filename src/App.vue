<script>
import AppHeader from "./components/AppHeader.vue";
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
  },
  methods: {
    requestData() {
      axios
        .get(
          `https://api.themoviedb.org/3/movie/550?api_key=95f92b62827d48d27c5483a9415a484d`
        )
        .then((response) => (this.store.cardList = response.data.data));
    },
  }

}




// https://api.themoviedb.org/3/movie/550?api_key=95f92b62827d48d27c5483a9415a484d
</script>

<template></template>

<style lang="scss"></style>
