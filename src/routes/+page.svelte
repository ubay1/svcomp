<script lang="ts">
	import TextField from '$lib/form/TextField.svelte';
</script>

<TextField id="username" name="username" label="username" placeholder="Masukan username" />

<!-- textHelper="ini text- helper"
	iconRequired={true}
	disabled={false}
	initialValue="ubay182"
	class={'border-1 border-error focus:outline-none'}
	errors={[]}
	nameError=""
  on:value={(value) => ($username = value?.detail ?? '')} -->

<style></style>
