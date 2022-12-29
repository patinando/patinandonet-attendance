<script lang="ts">
	import Textfield from '@smui/textfield';
	import HelperText from '@smui/textfield/helper-text';
	import Checkbox from '@smui/checkbox';
	import FormField from '@smui/form-field';
	import Button from '@smui/button';
	import Dialog, { Title, Content, Actions } from '@smui/dialog';

	let inputNames = '';
	let inputNamesArray: any[] = [];
	let checkedNames: any[] = [];
    let dialogTitle = '';
	let showDialog = false;
	let dialogContent = '';
    let numberOfGroups: number = 0;

	function handleInputNames() {
		inputNamesArray = inputNames.split('\n');
		// Clear whitespace
		inputNamesArray = inputNamesArray.map((name) => name.trim());
		// Remove empty strings
		inputNamesArray = inputNamesArray.filter((name) => name !== '');
		// Remove duplicates
		inputNamesArray = [...new Set(inputNamesArray)];
	}

	function handleRandomName() {
		dialogContent = inputNamesArray[Math.floor(Math.random() * inputNamesArray.length)];
        dialogTitle = 'Random Name';
		showDialog = true;
	}

    function handleGroups() {
        let groups: any[] = [];
        let names = [...inputNamesArray];
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
	<Textfield textarea bind:value={inputNames} on:change={handleInputNames}>
		<HelperText slot="helper">César Luis Juan Pedro</HelperText>
	</Textfield>

	<FormField>
		{#each inputNamesArray as name}
			<Checkbox {name} value={name} bind:group={checkedNames} />
			<label for={name}>{name}</label>
		{/each}
	</FormField>

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
