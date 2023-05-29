<script lang="ts">
  import { page } from '$app/stores';
  import { superForm } from 'sveltekit-superforms/client';
  import SuperDebug from 'sveltekit-superforms/client/SuperDebug.svelte'

  export let data;

  const {
    form,
    errors,
    enhance,
    message,
  } = superForm(data.form, {
		clearOnSubmit: 'none'
	});


	let menu = [
		'Cookies and cream',
		'Mint choc chip',
		'Raspberry ripple'
	];

  	function join(flavours) {
		if (flavours.length === 1) return flavours[0];
		return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`;
	}
</script>

<SuperDebug data={$form} />

<form method="POST" use:enhance>
	<h2>Size</h2>

	<label>
		<input type=radio bind:group={$form.scoops} name="scoops" value={1}>
		One scoop
	</label>

	<label>
		<input type=radio bind:group={$form.scoops} name="scoops" value={2}>
		Two scoops
	</label>

	<label>
		<input type=radio bind:group={$form.scoops} name="scoops" value={3}>
		Three scoops
	</label>

	{#if $errors.scoops}<p>{$errors.scoops}</p>{/if}

	<h2>Flavours</h2>

	{#each menu as flavour}
		<label>
			<input type=checkbox bind:group={$form.flavours} name="flavours" value={flavour}>
			{flavour}
		</label>
	{/each}

	{#if $errors.flavours}<p>{$errors.flavours}</p>{/if}

	{#if $message}<p>{$message}</p>{/if}
	<button>Submit</button>
</form>

<p class="info"><a href="https://svelte.dev/tutorial/group-inputs">Original code from Svelte documentation</a></p>

<style>
	.info {
		border-top: 1px solid gray;
		margin-top: 4rem;
	}
</style>