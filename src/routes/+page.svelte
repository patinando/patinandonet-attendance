<script lang="ts">
	import Textfield from '@smui/textfield';

	import Button from '@smui/button';
	import Dialog, { Title, Content, Actions } from '@smui/dialog';
	import InputNames from './InputNames.svelte';

	let checkedNames: string[] = [];

	let dialogTitle = '';
	let showDialog = false;
	let dialogContent = '';
	let numberOfGroups: number = 0;

	function handleRandomName() {
		dialogContent = checkedNames[Math.floor(Math.random() * checkedNames.length)];
		dialogTitle = 'Random Name';
		showDialog = true;
	}

	function handleGroups() {
		let groups: any[] = [];
		let names = [...checkedNames];
		let namesLength = names.length;
		let groupLength = Math.floor(namesLength / numberOfGroups);
		let remainder = namesLength % numberOfGroups;
		dialogContent = '';

		for (let i = 0; i < numberOfGroups; i++) {
			let group = [];
			for (let j = 0; j < groupLength; j++) {
				let randomIndex = Math.floor(Math.random() * names.length);
				group.push(names[randomIndex]);
				names.splice(randomIndex, 1);
			}
			groups.push(group);
		}

		for (let i = 0; i < remainder; i++) {
			let randomIndex = Math.floor(Math.random() * names.length);
			groups[i].push(names[randomIndex]);
			names.splice(randomIndex, 1);
		}
		console.log(groups);

		groups.forEach((group, index) => {
			dialogContent += `<span>Group ${index + 1}</span>`;
			group.forEach((name: string) => {
				dialogContent += `<p>${name}</p>`;
			});
		});
		dialogTitle = 'Groups';
		showDialog = true;
	}
</script>

<div class="margins">
	<InputNames bind:values={checkedNames} />

	<Button on:click={handleRandomName}>Random</Button>

	<Textfield bind:value={numberOfGroups} label="Number" type="number" />

	<Button on:click={handleGroups}>Groups</Button>

	<Dialog bind:open={showDialog} aria-labelledby="simple-title" aria-describedby="simple-content">
		<!-- Title cannot contain leading whitespace due to mdc-typography-baseline-top() -->
		<Title>{dialogTitle}</Title>
		<Content>{@html dialogContent}</Content>
		<Actions>
			<Button on:click={() => (showDialog = false)}>Close</Button>
		</Actions>
	</Dialog>
</div>
