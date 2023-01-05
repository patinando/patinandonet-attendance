<script lang="ts">
	import Textfield from '@smui/textfield';
	import HelperText from '@smui/textfield/helper-text';
	import Checkbox from '@smui/checkbox';
	import FormField from '@smui/form-field';
	import { page } from '$app/stores';

	export let checkedNames: string[] = [];
	let inputNames = '';
	let inputNamesArray: string[] = [];

	if ($page.url.searchParams.has('names')) {
		inputNames = $page.url.searchParams.get('names')?.split(',').join('\n') || '';
		inputNamesArray = inputNames.split('\n');
	}

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

<div class="container columns is-mobile">
	<div class="column">
		<Textfield textarea bind:value={inputNames} on:change={handleInputNames} />
	</div>

	<div class="column">
		<FormField>
			<div class="items">
				{#each inputNamesArray as name}
					<div class="item">
						<Checkbox {name} value={name} bind:group={checkedNames} />
						<label for={name}>{name}</label>
					</div>
				{/each}
			</div>
		</FormField>
	</div>
</div>

<style>
	.column {
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.item {
		display: flex;
		align-items: center;
	}
</style>
