<script lang="ts">
	import InputNames from './InputNames.svelte';
	import Dialog from './Dialog.svelte';
	import Random from './Random.svelte';
	import Groups from './Groups.svelte';

	let checkedNames: string[] = [];
	let dialogTitle: string = '';
	let showDialog: boolean = false;
	let dialogContent = '';
</script>

<div class="container">
	<section class="section">
		<h1 class="title">Random name and group</h1>
		<h2 class="subtitle">
			This app helps you to randomly select a name from a list of names, and create a group of
			people.
		</h2>
	</section>

	<InputNames bind:checkedNames />

	<div class="container columns is-mobile">
		<Random bind:dialogTitle bind:showDialog bind:dialogContent {checkedNames} />

		<Groups bind:dialogTitle bind:showDialog bind:dialogContent {checkedNames} />
	</div>

	<Dialog bind:dialogTitle bind:showDialog bind:dialogContent />
</div>
