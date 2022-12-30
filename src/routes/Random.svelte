<script lang="ts">
	import Button from '@smui/button';

	export let checkedNames: string[] = [];
	export let dialogTitle: string = '';
	export let showDialog: boolean = false;
	export let dialogContent = '';

	function handleRandomName() {
		dialogContent = checkedNames[Math.floor(Math.random() * checkedNames.length)];
		dialogTitle = 'Random Name';
		showDialog = true;
	}
</script>

<div>
	<Button on:click={handleRandomName}>Random</Button>
</div>
