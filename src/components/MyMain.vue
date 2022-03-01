<template>
  <main>

      <h2>Film</h2>
      <MyFilm :mostraRicerca="mostraRicerca" :movieChosen="movieChosen"/>

      <h2>Serie Televisive</h2>
      <MySeries :mostraRicercaSerie="mostraRicercaSerie" :tvChosen="tvChosen"/>

  </main>
</template>

<script>
import MyFilm from "./partials/MyFilm.vue"
import MySeries from "./partials/MySeries.vue"

export default {
    name: "MyMain",
    props: {
      'mostraRicerca': Array,
      'mostraRicercaSerie': Array,
      'tvChosen': Number,
      'movieChosen': Number
    },
    components: {
      MyFilm,
      MySeries
    }
}
</script>

<style scoped lang="scss">
main {
  margin-top: 30px;

  h2 {
    width: 70%;
    margin: 0 auto;
    padding: 50px 0;
  }
}

</style>