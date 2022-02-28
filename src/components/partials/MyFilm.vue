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

    data(){
        return{
            ricercaUtente: this.mostraRicerca,
            filmScelto: this.movieChosen
        }
    },

    computed: {
        filtroGeneri(){
            if (this.movieChosen == 0) {

                return this.ricercaUtente;

            } else {

                let filtro = [];

                for (let i=0; i<this.ricercaUtente.length; i++){

                    if (this.ricercaUtente[i].genre_ids.includes(this.filmScelto)){
                        filtro.push(this.ricercaUtente[i])
                    }
                }

                this.ricercaUtente = filtro;

                console.log(filtro);
                return filtro;
            } 
        }
    }
}
</script>

<style scoped lang="scss">
@import '~flag-icons/css/flag-icons.css';
@import '../../assets/style/cards.scss';

</style>