<template>
 
    <ul>
        <li v-for="(film, indice) in mostraRicerca" :key="indice">

            <div class="flip">

                <div class="front movie">
                
                    <img :src="`http://image.tmdb.org/t/p/w${widthMovie}${film.poster_path}`" :alt="film.title">

                </div> 

                <div class="back movie">

                    <h3 class="titolo">{{film.title}}</h3>
                    <h3 class="titolo-originale">{{film.original_title}}</h3>

                    <!-- aggiungo le bandiere in base alla lingua, se la lingua selezionata è l'inglese verrà fornito 'en' come risultato, in questo caso assegno la classe necessaria a visualizzare la bandiera UK visto che 'en' non è presente nelle flag-icons. In alternativa concateno l'inizio delle classi con l'appendice della lingua-->
                    <span :class="film.original_language == 'en'?'fi fi-gb' : `fi fi-${film.original_language}`"></span>

                    <span class="voto">{{film.vote_average}}</span>

                </div>
                
            </div>
        </li>
    </ul>

</template>

<script>
export default {
    name: "MyFilm",

    props: {
        "mostraRicerca": Array,
    },

    data(){
        return{
            widthMovie: 400
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
        width: 25%;
        height: 400px;
        background-color: transparent;
        border: 1px solid white;

        &:hover .flip {
            transform: rotateY(180deg); 
        }

        .flip {
            position: relative;
            width: 100%;
            height: 100%;
            transition: transform 0.6s;
            transform-style: preserve-3d;
            box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);

            .movie {
                position: absolute;
                width: 100%;
                height: 100%;
                -webkit-backface-visibility: hidden;
                backface-visibility: hidden;
            }

            .front img {
                width: 100%;
                height: 100%;
                object-fit: cover;
            }

            .back {
                transform: rotateY(180deg);
                background-color: black;
                display: flex;
                flex-direction: column;
                align-items: center;

                .titolo {
                    color: white;
                    text-align: center;
                    font-size: 1rem;
                }

                .titolo-originale {
                    color: white;
                    text-align: center;
                    font-size: 0.8rem;
                }

                .voto {
                    color: white;
                }
            }
        }
    }
}
</style>