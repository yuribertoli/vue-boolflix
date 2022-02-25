<template>
  <div id="app">
    <MyHeader @invioRicerca="getAxios"/> <!-- ricevo da Header il valore della ricerca tramite $emit invioRicerca, chiamo poi la funzione getAxios -->
    <MyMain :mostraRicerca="film" :mostraRicercaSerie="serie" /> <!-- invio a Main l'array film e serie tramite le props -->
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
      serie: []
    }
  },
  methods: {

    getAxios(valore){

      //popolo la variabile endpointSearch con il valore scritto dall'utente
      this.endpointSearch = valore;
      console.log("La ricerca dell'utente è: " + this.endpointSearch);

      //creo dinamicamente il percorso per i film
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

      //creo dinamicamente il percorso per le serie televisive
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.endpointKey}&language=${this.endpointChooseLanguage}&query=${this.endpointSearch}`)
      .then((response) => {
        console.log(response);

        //prendo solo l'array delle serie televisive
        this.serie = response.data.results;
        console.log(this.serie);
      })
      .catch((error) => {
        console.log(error);
      });
    }
  }
}

</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
