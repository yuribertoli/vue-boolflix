<template>
 
    <ul>
        <li v-for="(item, indice) in filtroGeneri" :key="indice">

            <MyCard :film="item"/>

        </li>
    </ul>

</template>

<script>
import MyCard from './cards/MyCard.vue'

export default {
    name: "MyFilm",

    components: {
        MyCard        
    },

    props: {
        "mostraRicerca": Array,
        'movieChosen': Number
    },

    computed: {
        filtroGeneri(){ //se il valore del genere scelto è 0 (quindi l'utente ha selezionato "Tutti i film" option)
                        //oppure se è null (quindi all'avvio del DOM quando non ci sono ancora state scelte da parte dell'utente)
            if (this.movieChosen == 0 || this.movieChosen == null) {

                return this.mostraRicerca; //mostro l'array completo

            }  else {

                //in tutti gli altri casi mostro solo i film (quindi l'oggetto dell'array che gli contiene)
                //filtrati tramite un array dove contengono i codici dei generi film, se corrispondono al codice del genere scelto dall'utente allora li mostro
                return this.mostraRicerca.filter( oggetto => {
                    return oggetto.genre_ids.includes(this.movieChosen);
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