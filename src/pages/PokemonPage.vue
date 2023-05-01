<template>
    <h3 v-if="!pokemon">Espere por favor ...</h3>
  <div v-else>
        <h1>Quien es este Pokemon?</h1>
        <div>

            <Picture :pokemonId="pokemon.id" :showPokemon="show" /> 
            <!-- La property tambien se puede mandar con v-bind:property -->
            <Options :pokemons="pokeArr" @selection="check($event)"/>

            <h4 class="fade-in">{{ message }}</h4>
            <button class="fade-in" v-if="answer" @click="replay">
                Nuevo Juego
            </button>

        </div>
  </div>
</template>

<script>
import Picture from '@/components/PokemonPicture.vue';
import Options from '@/components/PokemonOptions.vue';
import getPkOptions from '@/helpers/getPkOptions'

export default {
    components:{
        Picture,
        Options
    },
    data(){
        return {
            pokeArr: [],
            pokemon: null,
            show: false,
            answer: false,
            message: ''
        }
    },
    methods:{
        async pokeMix(){
            this.pokeArr = await getPkOptions()

            const numberRandom = Math.floor(Math.random() * 4)
            this.pokemon = this.pokeArr[ numberRandom ]
        },
        check(pokemonId){
            console.log('Respuesta', pokemonId)
            this.show = true
            this.answer = true
            pokemonId == this.pokemon.id ? this.message = `Bien! El pokemon es ${this.pokemon.name}` : this.message = `Oops, era ${this.pokemon.name}`
        },
        replay(){
            this.show = false
            this.answer = false
            this.pokeArr = []
            this.pokemon = null
            this.pokeMix()
        }
    },
    mounted(){
        this.pokeMix()
    }

}
</script>

<style scoped>
    button{
        padding: 5px 15px;
        border-radius: 9px;
        background-color: white;
    }
</style>
