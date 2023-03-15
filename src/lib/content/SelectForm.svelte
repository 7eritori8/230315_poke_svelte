<script lang="ts">
	import { SelectedPokemonStore } from '../module/SelectedPokemon/selectedPokemonStore.js';
	const pokemonIDArray = [133, 134, 135, 136, 196, 197, 470, 471, 700];
	let selected = '';

	function onsSubmit() {
		SelectedPokemonStore.update((n) => {
			n = selected;
			return n;
		});
	}
</script>

<h1>{$SelectedPokemonStore}</h1>
<select
	bind:value={selected}
	name="poke"
	on:change={() => {
		onsSubmit();
	}}
>
	{#each pokemonIDArray as pokemonID}
		<option value={pokemonID}>{pokemonID}</option>
	{/each}
</select>
