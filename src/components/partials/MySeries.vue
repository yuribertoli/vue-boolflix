<template>
  <ul>
        <li v-for="(item, indice) in mostraRicercaSerie" :key="indice">

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

    data(){
        return{

        }
    },

    props: {
        "mostraRicercaSerie": Array,
        'tvChosen': Number
    },

    computed: {

    }
}
</script>

<style scoped lang="scss">
@import '~flag-icons/css/flag-icons.css';
@import '../../assets/style/cards.scss';

</style>