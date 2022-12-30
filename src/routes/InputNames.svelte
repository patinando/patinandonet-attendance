<script lang="ts">
	import Textfield from '@smui/textfield';
	import HelperText from '@smui/textfield/helper-text';
	import Checkbox from '@smui/checkbox';
	import FormField from '@smui/form-field';

	let inputNames = '';
	let inputNamesArray: string[] = [];
	export let checkedNames: string[] = [];

	function handleInputNames() {
		inputNamesArray = inputNames.split('\n');
		// Clear whitespace
		inputNamesArray = inputNamesArray.map((name) => name.trim());
		// Remove empty strings
		inputNamesArray = inputNamesArray.filter((name) => name !== '');
		// Remove duplicates
		inputNamesArray = [...new Set(inputNamesArray)];
	}
</script>

<div>
	<Textfield textarea bind:value={inputNames} on:change={handleInputNames}>
		<HelperText slot="helper">César Luis Juan Pedro</HelperText>
	</Textfield>

	<FormField>
		{#each inputNamesArray as name}
			<Checkbox {name} value={name} bind:group={checkedNames} />
			<label for={name}>{name}</label>
		{/each}
	</FormField>
</div>
