<template>
 
    <ul>
        <li v-for="(film, indice) in mostraRicerca" :key="indice">
        <!-- <img :src="`http://image.tmdb.org/t/p/w${widthMovie}${film.poster_path}`" :alt="film.title"> -->
            <h3 class="titolo">{{film.title}}</h3>
            <h3 class="titolo-originale">{{film.original_title}}</h3>

            <!-- aggiungo le bandiere in base alla lingua  -->
            <span :class="film.original_language == 'en'?'fi fi-gb' : `fi fi-${film.original_language}`"></span>
            <span class="voto">{{film.vote_average}}</span>
        </li>
    </ul>

</template>

<script>
export default {
    name: "MyFilm",

    props: {
        "mostraRicerca": Array
    },

    data(){
        return{
            widthMovie: 200
        }
    },

    methods: {
        getClass(){
            return 
        }
    }
}
</script>

<style scoped lang="scss">
@import '~flag-icons/css/flag-icons.css';

ul {
    width: 70%;
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;

    li {
        width: calc(100% / 3);
        display: flex;
        flex-direction: column;
        align-items: center;
        height: 300px;
        border: 1px solid black;
        background-color: wheat;


    }
}
</style>