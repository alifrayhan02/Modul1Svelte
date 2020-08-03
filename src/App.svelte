<script>
	// video 3
	let name = "Mamank";
	// ------------
	import Surname from "./Surname.svelte";

	import UserInfo from "./UserInfo.svelte";

	import Box from "./Box.svelte";

	import Box2 from "./Box2.svelte";

	let stringToRender = "";

	let displayInfoMessage = false;

	import { slide,fade } from "svelte/transition";

	let count = 0;
	$: squared = count ** 2;
	$: squaredMinusOne = squared - 1;
	function handleClick() {
		count += 1;
	}

	let cities = [
		{
			id: "7891",
			name: "Blitar"
		},
		{
			id: "5479",
			name: "Jember"
		},
		{
			id: "4687",
			name: "Malang"
		},
		{
			id: "4897",
			name: "Surabaya"
		}
	]

	async function getRandomStarWarsCharacter() {
	const randomNumber = Math.floor(Math.random() * 10) + 1;
	const apiResponse = await fetch(
		`https://swapi.dev/api/people/${randomNumber}/`
	);	
	return await apiResponse.json();
	}
	let promise = getRandomStarWarsCharacter();


	let nama;
	function handleClick1() {
		alert("Hai " + nama);
	}
	function handleInput(event) {
		nama = event.target.value;
	}

	import {onMount} from 'svelte';
	let characters = [];
	onMount(async () => {
		const apiResponse = await fetch ("https://swapi.dev/api/people/");
		const swPeopleJSON = await apiResponse.json();
		characters = swPeopleJSON.results;
		return () =>console.log('Destroyed');
	});

	import { store } from "./store";
	import Incrementer from "./Incrementer.svelte";
	import Decrementer from "./Decrementer.svelte";
	import Setter from "./setter.svelte";

	import { tweened } from "svelte/motion";
	import { bounceInOut } from "svelte/easing";
	const progress = tweened(0, {
		duration: 2000,
		easing: bounceInOut
	});

</script>



<style>
	.headerText {
		color: powderblue;
		font-family: "Open Sans";
	}
	textarea {
		width: 100%;
		height: 12rem;
	}
</style>




<h1 class="headerText">Hello {name} !</h1>
<Surname/>

<UserInfo surname={'Kowalski'} />

<Box>
	<h1>Hello Guys !</h1>
	<p>Desc</p>
</Box>

<Box2>
	<h1 slot="header">Title of the page</h1>
	<span slot="body"></span>
	<span slot="footer">This is Footer</span>
</Box2>

<textarea bind:value={stringToRender} />

<div>{stringToRender}</div>

<form>
	<div class="name-field">
		<label for="name">Name :</label>
		<input type="text" name="name" />
	</div>
	<div class="surname-field">
		<label for="surname">Surname :</label>
		<input type="text" name="surname" />
	</div>
	<label>
		<input type="checkbox" bind:checked={displayInfoMessage} />
		Do You Want 1 Juta Dollar ?
	</label>
</form>

{#if displayInfoMessage}
	<h1 transition:fade={{ duration: 1000, delay:50}}>Makasih Lur :)</h1>
{/if}

<button on:click={handleClick}>Counter {count}</button>
<h1>Square of the counter is {squared}</h1>
<h1>Square is minus one {squaredMinusOne}</h1>

<h1>Provinsi Jawa Rumit</h1>
<ul>
	{#each cities as {id, name}, index}
	<li>{index + 1}: {name} (id: {id})</li>
	{/each}
</ul>


{#await promise}
	<h1>Loading...</h1>
{:then character}
	<h1>{character.name}</h1>
{/await}

<h1>Perkenalkan Nama anda:</h1>
<input type="text" on:change={handleInput} />
<button on:click|preventDefault={handleClick1}>Click Me</button>

<ul>
	{#each characters as {name, height, birth_year} }
		<li>
			<strong>{name}</strong>
			(height: {height} cm, Birth year: {birth_year})
		</li>
		{:else}
		<p>Loading...</p>
	{/each}
</ul>

<h1>The Count is {$store}</h1>
<Incrementer />
<Decrementer />
<Setter />

<h1>Installing Windows XP</h1>
<progress value={$progress} />
<sub>2 Week Remaining</sub>

<button on:click={() => progress.set(0)}>0%</button>
<button on:click={() => progress.set(0.5)}>50%</button>
<button on:click={() => progress.set(0.75)}>75%</button>
<button on:click={() => progress.set(1.0)}>100%</button>
{#if $progress === 1.0}
	<h1>The Windows XP Installed mantap gan</h1>
{/if}