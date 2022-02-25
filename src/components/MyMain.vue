<template>
  <main>

      <h2>Film</h2>
      <MyFilm :mostraRicerca="mostraRicerca" />

      <h2>Serie Televisive</h2>
      <MySeries :mostraRicercaSerie="mostraRicercaSerie" />

  </main>
</template>

<script>
import MyFilm from "./partials/MyFilm.vue"
import MySeries from "./partials/MySeries.vue"

export default {
    name: "MyMain",
    props: {
      'mostraRicerca': Array,
      'mostraRicercaSerie': Array
    },
    components: {
      MyFilm,
      MySeries
    },
    data(){
        return{

        }
    },
    methods: {

    }
}
</script>

<style scoped lang="scss">

</style>