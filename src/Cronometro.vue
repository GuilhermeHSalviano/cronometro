<template>
    <div id="corpo">
        <section class="container">
            <div class="cronometro">
                <div class="cronometro-relogio">
                    <span class="hms">{{ horas }}</span>
                    <span>{{ btnText }}</span>
                    <span class="hms">{{ minutos }}</span>
                    <span>{{ btnText }}</span>
                    <span class="hms">{{ segundos }}</span>
                </div>
                <div class="cronometro-botoes">
                    <button class="botoes" v-on:click="interruptor()" v-bind:class="classeBotao">{{ botaoDeAtivacao }}</button>
                    <button class="botoes botao-desativado" v-on:click="zerar()">Zerar</button>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
export default{
    data(){
        return{
            contador: 0,
            switch:false,
            delay: null,
            botaoDeAtivacao: "Iniciar",
            classeBotao: "botao-desativado"
        }
    },
    methods:{
        iniciar(){
            this.delay = setInterval(()=> {
                this.contador++
            }, 1000) 
        },
        parar(){
            clearInterval(this.delay)
            this.delay = null
        },
        interruptor(){
            if (this.delay == null){
                this.iniciar()
                this.botaoDeAtivacao = "Parar"
                this.classeBotao = "botao-ativado"
            } else {
                this.parar()
                this.botaoDeAtivacao = "Iniciar"
                this.classeBotao = "botao-desativado"
            }
        },
        zerar(){
            clearInterval(this.delay)
            this.delay = null
            this.contador = 0
        }
    },
    computed:{
        segundos(){
            return this.contador % 60
        },
        minutos(){
            return parseInt(this.contador/60) % 60
        },
        horas(){
            return parseInt(this.contador/3600)
        }
    },
    props: ['btnText']
}

</script>

<style>
    #corpo{
        align-items: center;
        background-color: var(--cinza-claro);
        display: flex;
        height: calc(100vh - 15vh);
        justify-content: center;
    }

    .container{
        align-items: center;
        background-color: white;
        display: flex;
        justify-content: center;
        height: 85%;
        width: 95%;
    }
    .cronometro{
        display: flex;
        flex-direction: column;
        height: 50%;
        padding-bottom: 10rem;
        width: 40%;
    }

    .cronometro-relogio{
        align-items: center;
        display: flex;
        font-family: var(--fonte-titulo);
        height: 80%;
        justify-content: space-around;
        width: 100%;
    }

    .hms{
        align-items: center;
        display: flex;
        font-size: 3.5rem;
        height: 6rem;
        justify-content: center;
        width: 6rem;
    }

    .horas{
        margin-left: 3rem;
    }

    .centesimos{
        height: 2.5rem;
        margin-right: 3rem;
        width: 2.5rem;

    }
    
    .cronometro-botoes{
        align-items: center;
        display: flex;
        height: 20%;
        justify-content: space-evenly;
        width: 100%;
    }

    .botoes{
        height: 80%;
        width: 25%;
        border-style: none;
    }

    .botoes:hover{
        cursor: pointer;
        background-color: var(--cinza-hover);
    }

    .botao-ativado{
        background-color: red;
        color: white;
    }

    .botao-desativado{
        background-color: grey;
        color: black;
    }

</style>
