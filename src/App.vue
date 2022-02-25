<template>
  <div id="app">
    <MyHeader/>
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
      endpointBeginning: "https://api.themoviedb.org/3/search/movie?api_key=",
      endpointKey: "2bec85c057b8f21a5e08ba0390ff42d0",
      endpointQuery: "&query=",
      endpointSearch: "",
      endpointLanguage: "&language=",
      endpointChooseLanguage: ""
    }
  },
  methods: {

      getAxios(){

        //creo dinamicamente il percorso 
        axios.get(this.endpointBeginning + 
                  this.endpointKey + 
                  this.endpointQuery + 
                  this.endpointSearch + 
                  this.endpointLanguage + 
                  this.endpointChooseLanguage)

        .then((response) => {
          console.log(response);
        })

        .catch((error) => {
          console.log(error);
        });
      }
  }
}
</script>

<style lang="scss">

</style>
