<template>
    <header> 

        <div class="left-header">
            <h1>BOOLFLIX</h1>
        </div>

        <!-- richiamo la funzione ricerca sia al click del bottone, sia alla pressione del tasto Enter(Invio) -->
        <div class="right-header">

            <!-- prendo il valore dell'opzione selezionata tramite v-model, invio ad App tramite $emit il cambio di valore -->  
            <select v-model.number="selectSerie" @change="$emit('genSeries', selectSerie)">
                <option value="0">Generi Serie TV</option>
                <option v-for="(genere, indice) in generiSerie" :key="indice" :value="genere.id">{{genere.name}}</option>
            </select>

            <select v-model.number="selectMovie" @change="$emit('genMovie', selectMovie)">
                <option value="0">Generi Film</option>
                <option v-for="(genere, indice) in generiFilm" :key="indice" :value="genere.id">{{genere.name}}</option>
            </select>

            <input v-on:keyup.enter="ricerca" type="text" v-model="cerca">
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
            selectSerie: null,
            selectMovie: null
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
    height: 50px;
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
</style>