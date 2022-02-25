<template>
 
    <ul>
        <li v-for="(film, indice) in mostraRicerca" :key="indice">
        <!-- <img :src="`http://image.tmdb.org/t/p/w${widthMovie}${film.poster_path}`" :alt="film.title"> -->
            <h3 class="titolo">{{film.title}}</h3>
            <h3 class="titolo-originale">{{film.original_title}}</h3>
            <span class="lingua">{{film.original_language}}</span>
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
    }
}
</script>

<style scoped lang="scss">

</style>