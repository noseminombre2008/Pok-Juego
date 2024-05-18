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
const streack = ref<number>(0)

const mixPokemonArray = async () => {
  pokemonArr.value = await getPokemonOptions()
  const randomInt = Math.floor(Math.random() * 4)
  pokemon.value = pokemonArr.value[randomInt]
  console.log(pokemon.value)
  console.log(pokemonArr.value)
}

const checkAnswer = (selectedId: number) => {
  showPokemon.value = true
  showAnswer.value = true

  if (selectedId === pokemon.value?.id) {
    streack.value++
    message.value = `Correcto, era un ${pokemon.value.name}`
  } else {
    streack.value = 0
    const motivationalMassges = [
    `Tu mamá no te quiere, eso es un ${pokemon.value.name}`,
    `Eres una come mrd, eso es un ${pokemon.value.name}`,
    `Gafo, tu novia quedo embrazada de otro por no saber que era una ${pokemon.value.name}`
    ]
    const randomInt = Math.floor(Math.random() * motivationalMassges.length)
    message.value = motivationalMassges[randomInt] 
  }
}

const newGame =()=>{
  showPokemon.value = false
  showAnswer.value = false
  pokemonArr.value = []
  pokemon.value = undefined

  mixPokemonArray()
}

mixPokemonArray()
</script>

<template>
  <div class="m-12">
    <PokemonPicture :show-pokemon="showPokemon" v-if="pokemon" :pokemon-id="pokemon.id" />
    <div class="flex justify-center text-4xl font-bold mt-12"> 
      <p>{{ streack }}</p>
      <p class="text-blue-400" v-if="streack == 10 ">Cuiden a su novia, este si le sabe</p>
    </div>
    <PokemonOptions @selection-pokemon="checkAnswer" :pokemons="pokemonArr" />
  </div>
  <div v-if="showAnswer" class="flex flex-col text-center space-y-6">
    <p class="text-3xl font-bold">{{ message }}</p>
    <butoon class="border-4 p-2 rounded-2xl" @click="newGame">Nuevo Juego</butoon> 
  </div>
</template>
