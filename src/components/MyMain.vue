<template>
  <main>
      <MyFilm :mostraRicerca="mostraRicerca"/>
  </main>
</template>

<script>
import MyFilm from "./partials/MyFilm.vue"

export default {
    name: "MyMain",
    props: {
      'mostraRicerca': Array
    },
    components: {
      MyFilm
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