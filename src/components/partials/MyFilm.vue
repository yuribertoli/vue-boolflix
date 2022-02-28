<template>
 
    <ul>
        <li v-for="(item, indice) in mostraRicerca" :key="indice">

            <MyCard :film="item"/>

        </li>
    </ul>

</template>

<script>
import MyCard from './MyCard.vue'

export default {
    name: "MyFilm",

    components: {
        MyCard
    },

    props: {
        "mostraRicerca": Array,
    }
}
</script>

<style scoped lang="scss">
@import '~flag-icons/css/flag-icons.css';
@import '../../assets/style/cards.scss';

</style>