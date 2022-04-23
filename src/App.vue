<template>
    <div>
        <navegador></navegador>
        <cronometro v-bind:btn-text= text></cronometro>
    </div>
</template>

<script>
import Navegador from "./Navegador.vue"
import Cronometro from "./Cronometro.vue"
export default{
    data () {
        return{
            text: ":"
        }
    },
    components:{
        Navegador,
        Cronometro,
    },  
}
</script>

<style>
@import "./variaveis.css";
</style>
