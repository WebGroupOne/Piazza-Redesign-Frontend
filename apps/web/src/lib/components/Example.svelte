<script lang="ts">
	// This is how we declare props (ie. data we want to pass into this component)
	export let prop: string;

	// Some state that will be forwarded to any children
	let num = 0;
</script>

<div>
	<p>textIn as prop = {prop}</p>
	<p>num = {num}</p>
	<button on:click={() => num++}>Update Num</button>

	<!-- Slot allows us to insert child components -->
	<!-- Any child component now gets access to num -->
	<slot {num} />
</div>
