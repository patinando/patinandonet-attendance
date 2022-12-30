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

<div class="margins">
	<InputNames bind:checkedNames />

	<Random bind:dialogTitle bind:showDialog bind:dialogContent {checkedNames} />

	<Dialog bind:dialogTitle bind:showDialog bind:dialogContent />

	<Groups bind:dialogTitle bind:showDialog bind:dialogContent {checkedNames} />
</div>
