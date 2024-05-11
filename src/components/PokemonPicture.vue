<template>
    <div class="flex justify-center">
     <img :src="img" alt="img-pokemon">
    </div>
</template>

<script lang="ts" setup>
 const props = defineProps<{
        pokemonId: number
    }>()

    const img = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${ props.pokemonId }.svg`;
</script>