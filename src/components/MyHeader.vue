<template>
    <header> 

        <div class="left-header">
            <h1>BOOLFLIX</h1>
        </div>

        <!-- richiamo la funzione ricerca sia al click del bottone, sia alla pressione del tasto Enter(Invio) -->
        <div class="right-header">

            <div class="mediaquery">
                <!-- creo una lista di lingue tra cui l'utente puo' scegliere per le descrizioni dei film/serie -->
                <div class="contain">
                    <i class="fas fa-chevron-down"></i>
                    <h5 id="title-sel">Selezioni:</h5>
                    <h5>{{this.lingua.linguaText == null? "Inglese" : this.lingua.linguaText}}</h5> <!-- se la ricerca della lingua non è stata fatta, lascio inglese come default (l'opzione inglese ha valore vuoto, quindi null) -->
                    <h3 id="lingua"><span>Scegli</span> Lingua</h3>
                    <select v-model="lingua" @change="$emit('langSelected', lingua.valoreLingua)">
                        <option v-for="(language, index) in lingueDaMostrare" :key="index" :value="language">{{language.linguaText}}</option>
                    </select>                                                           <!-- setto il value come un oggetto per poterne ricavare sia il valore numerico che il testo mostrato in contesti diversi -->
                </div>

                <!-- prendo il valore dell'opzione selezionata tramite v-model, invio ad App tramite $emit il cambio di valore --> 
                <div class="contain">
                    <i class="fas fa-chevron-down"></i>
                    <h5>{{this.selectMovie.name == null? "Tutti" : this.selectMovie.name}}</h5> <!-- se la ricerca del genere non è stata fatta, o è impostata sulla prima opzione "Tutti i film", lascio "Tutti" come default (la prima opzione ha un value = 0, quindi null) -->
                    <h3 id="film"><span>Generi</span> Film</h3>
                    <select v-model="selectMovie" @change="$emit('genMovie', selectMovie.id)">
                        <option value="0">Tutti i Film</option>
                        <option v-for="(genere, indice) in generiFilm" :key="indice" :value="genere">{{genere.name}}</option>
                    </select>                                                        <!-- setto il value come un oggetto per poterne ricavare sia il valore numerico che il testo mostrato in contesti diversi -->
                </div>

                <div class="contain">
                    <i class="fas fa-chevron-down"></i>
                    <h5>{{this.selectSerie.name  == null? "Tutti" : this.selectSerie.name}}</h5> <!-- se la ricerca del genere non è stata fatta, o è impostata sulla prima opzione "Tutte le serie", lascio "Tutti" come default (la prima opzione ha un value = 0, quindi null) -->
                    <h3 id="serie"><span>Generi</span> Serie TV</h3> 
                    <select v-model="selectSerie" @change="$emit('genSeries', selectSerie.id)">
                        <option value="0">Tutte le Serie TV</option>
                        <option v-for="(genere, indice) in generiSerie" :key="indice" :value="genere">{{genere.name}}</option>
                    </select>                                                         <!-- setto il value come un oggetto per poterne ricavare sia il valore numerico che il testo mostrato in contesti diversi -->
                </div>
            </div>

            <input v-on:keyup.enter="ricerca" type="text" v-model="cerca" placeholder="Cerca un titolo">
            <button @click="ricerca">CERCA</button>
        </div>

    </header>
</template>

<script>
const axios = require('axios').default

export default {
    name: "MyHeader",

    data(){
        return{
            cerca: "",
            endpointKey: "2bec85c057b8f21a5e08ba0390ff42d0",
            generiFilm: [],
            generiSerie: [],
            selectSerie: "",
            selectMovie: "",
            lingua: "",
            lingueDaMostrare: [
                {valoreLingua: "it-IT", linguaText: "Italiano"},
                {valoreLingua: "", linguaText: "Inglese"},
                {valoreLingua: "es-ES", linguaText: "Spagnolo"},
                {valoreLingua: "pt-PT", linguaText: "Portoghese"},
                {valoreLingua: "fr-FR", linguaText: "Francese"},
                {valoreLingua: "de-DE", linguaText: "Tedesco"},
                {valoreLingua: "ru-RU", linguaText: "Russo"},
                {valoreLingua: "zh-ZH", linguaText: "Cinese"},
                {valoreLingua: "ja-JA", linguaText: "Giapponese"},
                {valoreLingua: "ar-AR", linguaText: "Arabo"},
                {valoreLingua: "hi-HI", linguaText: "Hindi"},
            ]
        }
    },

    methods: {
        ricerca(){ //se il valore di cerca è diverso da vuoto invio ad App la stringa ricercata
            if (this.cerca != "") {
                this.$emit('invioRicerca', this.cerca);
            }
        }
    },

    created: function() {

        //Utilizzo un setTimeout per richiamare l'API alla creazione del DOM
        setTimeout(() => {

            //Prendo la lista generi per i film
            axios.get(`https://api.themoviedb.org/3/genre/movie/list?api_key=${this.endpointKey}`)

            .then((response) => {
                console.log(response);

                //prendo l'array dei generi
                this.generiFilm = response.data.genres;
                console.log(this.generiFilm);
            })
            .catch((error) => {
                console.log(error);
            });

            //Prendo la lista generi per le serie TV
            axios.get(`https://api.themoviedb.org/3/genre/tv/list?api_key=${this.endpointKey}`)

            .then((response) => {
                console.log(response);

                //prendo l'array dei generi
                this.generiSerie = response.data.genres;
                console.log(this.generiSerie);
            })
            .catch((error) => {
                console.log(error);
            });
         
        }, 0)
    }
}
</script>

<style scoped lang="scss">
header {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 999;
    height: 50px;
    width: 100%;
    background-color: black;
    display: flex;
    justify-content: space-between;
    align-items: center;

    h1 {
        color: red;
        padding-left: 40px;
    }
    
    .right-header {
        display: flex;
        align-items: center;

        .mediaquery {
            display: flex;

            .contain {
                display: flex;
                align-items: center;
                position: relative;

                    h3, span {
                        color: white;
                        font-size: 0.9rem;
                        font-weight: 600;
                    }

                    h5 {
                        position: absolute;
                        color: gray;
                        left: -1px;
                        top: 18px;
                        width: 130px;
                        font-size: 0.7rem;
                    }

                    #title-sel {
                        left: -60px;
                    }

                    select {
                    width: 23px;
                    background-color: black;
                    border-radius: 30%;
                    border: 2px solid grey;
                    margin: 0 20px 0 5px;
                    cursor: pointer;

                    option {
                        color: white;
                    }
                }

                svg {
                    position: absolute;
                    font-size: 0.8rem;
                    z-index: 88;
                    top: 2.5px;
                    right: 25.5px;
                    color: #e3e3e3;
                    pointer-events: none; /* permette di cliccare sotto questo elemento, rendendolo invisibile agli eventi */
                }
            }
        }

        input {
            width: 200px;
            &:focus {
                outline: none;
                border:1px solid rgba(255,0,0,0.5);
                box-shadow: 0 0 10px 5px rgba(255,0,0,0.5);
            }
        }

        button {
            width: 80px;
            margin-right: 40px;
            margin-left: 10px;
            font-size: 0.6rem;
            font-weight: 700;
            padding: 2px 0;
            border-radius: 3px;
            background-color: rgba(255,0,0,0.9);
            border-color: rgba(255,0,0,0.9);
        }
    }  
}

@import '../assets/style/mediaqueryHeader.scss';
</style>