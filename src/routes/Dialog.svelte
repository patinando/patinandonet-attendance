<script lang="ts">
	import Dialog, { Title, Content, Actions } from '@smui/dialog';
	import Button from '@smui/button';

	export let dialogTitle = '';
	export let showDialog = false;
	export let dialogContent = '';
</script>

<div>
	<Dialog bind:open={showDialog} aria-labelledby="simple-title" aria-describedby="simple-content">
		<Title>{dialogTitle}</Title>
		<Content>{@html dialogContent}</Content>
		<Actions>
			<Button on:click={() => (showDialog = false)}>Close</Button>
		</Actions>
	</Dialog>
</div>
