<template>
  <div id="app">
    <MyHeader @invioRicerca="getAxios"/>
    <MyMain/>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'

const axios = require('axios').default;

export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain
  },
  data(){
    return{
      endpointKey: "2bec85c057b8f21a5e08ba0390ff42d0",
      endpointSearch: "",
      endpointChooseLanguage: "it-IT",

      film: [],
      stringaRicevuta: ""
    }
  },
  methods: {

    getAxios(valore){

      //creo dinamicamente il percorso 
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.endpointKey}&language=${this.endpointChooseLanguage}&query=${this.endpointSearch}`)

      .then((response) => {
        console.log(response);

        //prendo solo l'array dei film
        this.film = response.data.results;
        console.log(this.film);
      })

      .catch((error) => {
        console.log(error);
      });

      this.stringaRicevuta = valore;
      console.log(this.stringaRicevuta);
    }
  }
}

</script>

<style lang="scss">

</style>
