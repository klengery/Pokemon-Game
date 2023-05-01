<template>
  <div class="pokemonContainer">
    <img :src="imgSrc" 
        class="hiddePokemon"
        alt="pokemon"
        v-if="!showPokemon"
    >

    <img 
        v-else
        :src="imgSrc"
        class="fade-in"
        alt="pokemon"
    >
  </div>
</template>

<script>
export default {
    computed:{
        imgSrc(){
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    },
    props:{
        pokemonId:{
            type: Number,
            required: true
        },
        showPokemon:{
            type: Boolean,
            required: true,
            default: false
        }
    }
}
</script>

<style scoped>
.hiddePokemon{
    filter:brightness(0)
}

.pokemonContainer {
    height: 200px;
}

img {
    height: 200px;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}
</style>