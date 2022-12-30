<script lang="ts">
	import Textfield from '@smui/textfield';

	import Button from '@smui/button';

	export let checkedNames: string[] = [];
	export let dialogTitle: string = '';
	export let showDialog: boolean = false;
	export let dialogContent = '';

	let numberOfGroups: number = 0;

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

<div>
	<Textfield bind:value={numberOfGroups} label="Number" type="number" />

	<Button on:click={handleGroups}>Groups</Button>
</div>
