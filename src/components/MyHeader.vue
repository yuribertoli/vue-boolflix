<template>
    <header> <!-- richiamo la funzione ricerca sia al click del bottone, sia alla pressione del tasto Enter(Invio) -->
        <input v-on:keyup.enter="ricerca" type="text" v-model="cerca">
        <button @click="ricerca">Cerca</button>
    </header>
</template>

<script>
export default {
    name: "MyHeader",
    props: {

    },  
    components: {
    
    },  
    data(){
        return{
            cerca: ""
        }
    },
    methods: {
        ricerca(){ //se il valore di cerca è diverso da vuoto invio ad App la stringa ricercata
            if (this.cerca != "") {
                this.$emit('invioRicerca', this.cerca);
            }
        }
    }
}
</script>

<style scoped lang="scss">

</style>