<script>
  import PokemanCard from '../components/pokemanCard.svelte';
  import { pokemon } from '../stores/pokestore';

  let searchTerm = ''
  let filteredPokemon = []

  $: {
    console.log(searchTerm)
    if (searchTerm) {
      filteredPokemon = $pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()))
    } else {
      filteredPokemon = [...$pokemon]
    }
  }
</script>

<svelte:head>
  <title>Svelte Kit Pokedex</title>
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>

<label class="hidden" for="poke-search">Search for a poekmon:</label>
<input class="w-full rounded-md text-lg p-4 border-2 border-gray-200" type="text" name="poke-search" id="poke-search" placeholder="Search Pokemon" bind:value={searchTerm}>

<div class="grid gap-4 mt-4 grid-cols-1 md:grid-cols-2">
  {#each filteredPokemon as pokeman}
    <PokemanCard pokeman={pokeman}/>
  {/each}
</div>

<style lang="postcss">
  :global(html) {
    background-color: theme(colors.gray.100);
  }
</style>