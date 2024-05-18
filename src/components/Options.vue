<template>
  <div class="grid grid-cols-2 gap-12 items-center mx-32 mt-6 space-y-1">
    <button
      @click="$emit('selectionPokemon', pokemon.id)"
      class="text-3xl border-4 p-2 rounded-2xl"
      v-for="pokemon in pokemons"
      :key="pokemon.id"
    >
      {{ pokemon.name }}
    </button>
  </div>
</template>

<script lang="ts" setup>
import type { Pokemon } from 'env'

defineProps<{
  pokemons: Pokemon[]
}>()
</script>
