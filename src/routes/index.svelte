<script context="module">
  export async function load({page}){
    const url = `https://pokeapi.co/api/v2/pokemon?limit=${151}`;
    const res = await fetch(url);
    const data = await res.json();
    const loadedPokemon = data.results.map((data, index) => {
        return {
            name: data.name,
            id: index + 1,
            image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`
        };
    });
    return {props: { pokemon:loadedPokemon}};
  }
</script>
<script>
  import PokemanCard from '../components/pokemanCard.svelte';
  export let pokemon; //Loaded through SSR in async function load

  let searchTerm = "";
  let filteredPokemon = [];

  $: {
    if (searchTerm) {
      //Search for pokemon
      filteredPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()));
    } else {
      filteredPokemon = [...pokemon];
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