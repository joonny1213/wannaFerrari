<script>
	let files;

	$: if (files) {
		// Note that `files` is of type `FileList`, not an Array:
		// https://developer.mozilla.org/en-US/docs/Web/API/FileList
		console.log(files);

		for (const file of files) {
			console.log(`${file.name}: ${file.size} bytes`);
		}
	}
</script>
<style>
	label{
		font-size: 4em;
		font-family: 'Comic Sans MS', serif;
	}
</style>
<br><br><br>
<label for="many">Select files to upload to firebase</label>
<input
	bind:files
	id="many"
	multiple
	type="file"
/>
{#if files}
	<h2>Selected files:</h2>
	{#each Array.from(files) as file}
		<p>{file.name} ({file.size} bytes) </p>
	{/each}
{/if}