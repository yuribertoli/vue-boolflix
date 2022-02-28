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

                    <span class="voto">Voto: {{serie.vote_average}}</span>

                    <div class="stars">

                        <div class="stelle" v-if="serie.vote_average >= 0 && serie.vote_average < 1">
                            <!-- mezza stella tra 0 e 1 --> <i class="fas fa-star-half-alt"></i> 
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 1 && serie.vote_average < 2">
                            <!-- una stella tra 1 e 2 --> <i class="fas fa-star"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 2 && serie.vote_average < 3">
                            <!-- una stella e mezza tra 2 e 3 --> <i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 3 && serie.vote_average < 4">
                            <!-- due stelle tra 3 e 4 --> <i class="fas fa-star"></i><i class="fas fa-star"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 4 && serie.vote_average < 5">
                            <!-- due stelle e mezzo tra 4 e 5 --> <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 5 && serie.vote_average < 6">
                            <!-- tre stelle tra 5 e 6 --> <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 6 && serie.vote_average < 7">
                            <!-- tre stelle e mezzo tra 6 e 7 --><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 7 && serie.vote_average < 8">
                            <!-- quattro stelle tra 7 e 8 --><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 8 && serie.vote_average < 9">
                            <!-- quattro stelle e mezzo tra 8 e 9 --><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i>
                        </div>
                        <div class="stelle" v-else-if="serie.vote_average >= 9">
                            <!-- cinque stelle tra 9 e 10 --><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                        </div>

                    </div>

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