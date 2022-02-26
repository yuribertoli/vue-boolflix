<template>
  <ul>
        <li v-for="(serie, indice) in mostraRicercaSerie" :key="indice">

            <div class="flip">

                <div class="front movie">

                    <img :src="`http://image.tmdb.org/t/p/w${widthMovie}${serie.poster_path}`" :alt="serie.name">

                </div>

                <div class="back movie">

                    <h3 class="titolo">{{serie.name}}</h3>
                    <h3 class="titolo-originale">{{serie.original_name}}</h3>

                    <!-- aggiungo le bandiere in base alla lingua, se la lingua selezionata è l'inglese verrà fornito 'en' come risultato, in questo caso assegno la classe necessaria a visualizzare la bandiera UK visto che 'en' non è presente nelle flag-icons. In alternativa concateno l'inizio delle classi con l'appendice della lingua-->
                    <span :class="serie.original_language == 'en'?'fi fi-gb' : `fi fi-${serie.original_language}`"></span>

                    <span class="voto">{{serie.vote_average}}</span>

                    <h6>Trama</h6>

                    <p>{{serie.overview}}</p>

                </div>

            </div>

        </li>
  </ul>
</template>

<script>
export default {
    name: "MySeries",

    props: {
        "mostraRicercaSerie": Array
    },

    data(){
        return{
            widthMovie: 342
        }
    }
}
</script>

<style scoped lang="scss">
@import '~flag-icons/css/flag-icons.css';
@import '../../assets/style/cards.scss';

</style>