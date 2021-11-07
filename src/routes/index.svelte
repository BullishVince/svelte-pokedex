<script>
  import {pokemon} from '../stores/pokestore';
  import PokemanCard from '../components/pokemanCard.svelte';

  let searchTerm = "";
  let filteredPokemon = [];

  $: {
    if (searchTerm) {
      //Search for pokemon
      filteredPokemon = $pokemon.filter(pokeman => pokeman.name.includes(searchTerm));
    } else {
      filteredPokemon = [...$pokemon];
    }
  }
</script>

<style>
    @import 'tailwindcss/dist/tailwind.css';
</style>

<svelte:head>
  <title>Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">SvelteKit Pokedex</h1>

<input type="text" class="w-full rounded-md text-lg p-4 border-2 border-gray-200" 
placeholder="Search Pokemon" bind:value={searchTerm}>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
  {#each filteredPokemon as pokeman}
  <PokemanCard pokeman={pokeman}/>
{/each}
</div>