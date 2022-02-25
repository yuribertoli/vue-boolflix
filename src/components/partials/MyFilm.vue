<template>
 
    <ul>
        <li v-for="(film, indice) in mostraRicerca" :key="indice">
            <img :src="`http://image.tmdb.org/t/p/w${widthMovie}${film.poster_path}`" alt="">
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