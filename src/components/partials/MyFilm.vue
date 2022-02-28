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
        filtroGeneri(){
            if (this.movieChosen == 0) {

                return this.$props.mostraRicerca;

            } else {

                let filtro = [];

                for (let i=0; i<this.$props.mostraRicerca.length; i++){

                    if (this.$props.mostraRicerca[i].genre_ids.includes(this.$props.movieChosen)){
                        filtro.push(this.$props.mostraRicerca[i])
                    }
                }

                this.$props.mostraRicerca = filtro;

                console.log(filtro);
                return filtro;
            } 
        }
    },

    /* computed: {

        generiFiltrati(){

            console.log(this.$props.mostraRicerca);

            if (this.movieChosen == 0) {

                return this.mostraRicerca;

            } else {

                let filtro = [];

                for (let i=0; i<20; i++){

                    if (this.mostraRicerca[i].genre_ids.includes(this.movieChosen)){
                        filtro.push(this.mostraRicerca[i])
                    }
                }

                console.log(filtro);
                return filtro;
            } 
        }
    } */
}
</script>

<style scoped lang="scss">
@import '~flag-icons/css/flag-icons.css';
@import '../../assets/style/cards.scss';

</style>