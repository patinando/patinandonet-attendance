<script lang="ts">
	import Button from '@smui/button';
	import { writable } from 'svelte/store';

	export let checkedNames: string[] = [];
	export let dialogTitle: string = '';
	export let showDialog: boolean = false;
	export let dialogContent = '';

	let random = '';
	const historyRandom = writable<string[]>([]);

	function handleRandomName() {

		let loop = false;
		let allUsed = false;

		random = checkedNames[Math.floor(Math.random() * checkedNames.length)];
		historyRandom.subscribe((value) => {

			if (value.length === checkedNames.length) {
				console.log("all names have been used");
				allUsed = true;
			}

			console.log(value);
			if (value.includes(random)) {
				console.log("random name already exists");
				loop = true;
			}
		});

		if (allUsed) {
			dialogContent = 'All names have been used';
			dialogTitle = 'Random Name';
			showDialog = true;
			historyRandom.set([]);
			return;
		}

		if (loop) {
			handleRandomName();
		} else {
			historyRandom.update((value) => [...value, random]);
			dialogContent = random;
			dialogTitle = 'Random Name';
			showDialog = true;
		}
	}
</script>

<div>
	<Button on:click={handleRandomName}>Random</Button>
</div>
