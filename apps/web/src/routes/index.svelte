<script lang="ts">
	// You write TS Code in the script section... Make sure to use lang="ts" otherwise it will just default to JS
	// Multiple script sections can be used in the same file

	// Make sure to put any external components or ts files in the lib folder so that we can use this convienient $lib import syntax
	import Example from '$lib/components/Example.svelte';
	import { TEST_CLIENT_MODULE } from 'app-backend'; // app-backend is our module for Firebase logic
	import { onDestroy, onMount } from 'svelte';

	// State can be created with the let keyword
	let count = 0;

	// The $ denotes a reactive variable, countX2 will be updated whenever count changes
	$: countX2 = count * 2;

	const updateCount = () => count++;

	let textIn = '';

	const createItems = (amount: number) => {
		const items = [];
		for (let i = 0; i < amount; i++) {
			items.push('Item ' + i);
		}
		return items;
	};

	// On mount runs whenever the component is loaded for the first time
	onMount(() => {
		// Testing to see if the monorepo works correctly
		console.log(TEST_CLIENT_MODULE);
	});

	// On Destroy runs whenever the component is destroyed
	onDestroy(() => {
		console.log('Bye!');
	});
</script>

<!-- Use this to get access to the HTML head tag -->
<svelte:head>
	<title>Example App</title>
</svelte:head>

<h1>Look in index.svelte for examples on how svelte works if you're new to it</h1>
<p>Count is {count}</p>
<p>Count * 2 is {countX2}</p>
<button on:click={updateCount}>Update Count</button>

<!-- You can get access to DOM elements with the bind keyword -->
<p>textIn = {textIn}</p>
<input type="text" bind:value={textIn} />

<!-- Using a custom component example (anything inside here can access num which is a state from the example component) -->
<Example prop={textIn} let:num>
	<!-- Conditional Statements -->
	{#if count > 0}
		<!-- Iterate through a list of items -->
		{#each createItems(count) as item}
			<li>{item} and num = {num}</li>
		{/each}
	{:else}
		<p>Update Count to see some things here!</p>
	{/if}
</Example>

<!-- 
  Unlike React, CSS is scoped within the file that contains it, 
  the global keyword (which should be avoided most of the time) overrides this 
-->
<style lang="scss" global>
	/* Make sure to use lang="scss" to be able to use Sass in style sections */
	@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@700&display=swap');

	html {
		font-family: 'Raleway', sans-serif;
	}

	@mixin hello {
		color: red;
	}

	h1 {
		@include hello;
	}
</style>
