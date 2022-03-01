<template>
  <ul>
        <li v-for="(item, indice) in filtroGeneri" :key="indice">

            <MyCardSeries :serie="item"/>

        </li>
  </ul>
</template>

<script>
import MyCardSeries from './cards/MyCardSeries.vue'

export default {
    name: "MySeries",

    components: {
        MyCardSeries
    },

    props: {
        "mostraRicercaSerie": Array,
        'tvChosen': Number
    },

    computed: {
        filtroGeneri(){ //se il valore del genere scelto è 0 (quindi l'utente ha selezionato "Tutte le Serie TV" option)
                        //oppure se è null (quindi all'avvio del DOM quando non ci sono ancora state scelte da parte dell'utente)
            if (this.tvChosen == 0 || this.tvChosen == null) {

                return this.mostraRicercaSerie; //mostro l'array completo

            }  else {

                //in tutti gli altri casi mostro solo le serie (quindi l'oggetto dell'array che gli contiene)
                //filtrati tramite un array dove contengono i codici dei generi serie, se corrispondono al codice del genere scelto dall'utente allora li mostro
                return this.mostraRicercaSerie.filter( oggetto => {
                    return oggetto.genre_ids.includes(this.tvChosen);
                })
            }  
        }
    }
}
</script>

<style scoped lang="scss">
@import '~flag-icons/css/flag-icons.css';
@import '../../assets/style/cards.scss';

</style>