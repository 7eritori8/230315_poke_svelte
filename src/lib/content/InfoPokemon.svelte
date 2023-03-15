<script lang="ts">
	import { SelectedPokemonStore } from '../module/SelectedPokemon/selectedPokemonStore.js';

	// storeの値が変わったときになにかしたいときは、必ず$:

	// $:処理
	// ストア関係ない

	// $ストア名
	// ストアを参照するときに使う
	// subscribeとの違いは？２倍した値を表示したいときは、subscirbe
	$: console.log($SelectedPokemonStore);

	async function getPokeInfo(id) {
		let url = `https://pokeapi.co/api/v2/pokemon/${id}`;
		const res = await fetch(url);
		const text = await res.json();
		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}
	$: result = getPokeInfo($SelectedPokemonStore);
	let ans = '';
	let btw = '';
	let bar = '';
</script>

{#await result}
	<p class="load">Loading...</p>
{:then resultContent}
	<h1>{resultContent.name}</h1>
	<img src={resultContent.sprites.front_default} alt="" />
{/await}

<!-- templateの中は書き換わったものが即時表示 -->
<!-- しかし、上のscriptでは、内部的に書き換わっても、処理はされない -->
<!-- $:処理で書くとそれに関わる -->
<input type="text" bind:value={ans} />
<input type="text" bind:value={btw} />
<h1>{ans}</h1>
