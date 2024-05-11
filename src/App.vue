<script setup lang="ts">
import type { Pokemon } from 'env'
import getPokemonOptions from './api/getPokemonOptions'
import { ref } from 'vue'
import PokemonOptions from './components/Options.vue'
import PokemonPicture from './components/PokemonPicture.vue'

const pokemonArr = ref<Pokemon[]>([])
const pokemon = ref<Pokemon>()
const showPokemon = ref<boolean>(false)
const showAnswer = ref<boolean>(false)
const message = ref<string>()

const mixPokemonArray = async () => {
  pokemonArr.value = await getPokemonOptions()
  const randomInt = Math.floor(Math.random() * 4)
  pokemon.value = pokemonArr.value[randomInt]
  console.log(pokemon.value)
  console.log(pokemonArr.value)
}

const checkAnswer=(selectedId: number)=>{
  showPokemon.value = true
  showAnswer.value = true

  if(selectedId === pokemon.value?.id){
    message.value = `Correcto, era un ${pokemon.value.name}`
  }
  else{
    message.value = `Gafo, tu novia quedo embrazada de otro por no saber que era una ${pokemon.value.name}`
  }
}

mixPokemonArray()
</script>

<template>
  <div class="m-12">
    <PokemonPicture :show-pokemon="showPokemon" v-if="pokemon" :pokemon-id="pokemon.id" />
    <PokemonOptions @selection-pokemon="checkAnswer" :pokemons="pokemonArr" />
  </div>
<div class="text-center">
  <p class="text-2xl">{{ message }}</p>
</div>
</template>
