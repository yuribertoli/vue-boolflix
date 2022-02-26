<template>
    <header> <!-- richiamo la funzione ricerca sia al click del bottone, sia alla pressione del tasto Enter(Invio) -->

        <div class="left-header">
            <h1>BOOLFLIX</h1>
        </div>

        <div class="right-header">
            <input v-on:keyup.enter="ricerca" type="text" v-model="cerca">
            <button @click="ricerca">CERCA</button>
        </div>

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