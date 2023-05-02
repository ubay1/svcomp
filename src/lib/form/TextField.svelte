<script lang="ts">
	import { onMount, createEventDispatcher } from 'svelte';
	import ErrorMessage from './ErrorMessage.svelte';

	const dispatch = createEventDispatcher();

	export let id: string = '';
	export let label: string = '';
	export let name: string = '';
	export let placeholder: string = '';
	export let autocomplete: string = 'off';
	export let maxLength: number = 300;
	export let disabled: boolean = false;
	export let iconRequired: boolean = false;
	export let initialValue: string = '';
	export let textHelper: string = '';
	export let isUpperCase: boolean = false;
	export let errors: string[] = [];
	export let nameError: string = '';
	// export let minChar: number = 0;
	// export let idConfirm: string = '';
	// export let customError: string = '';

	let value = '';

	$: value = initialValue;
	$: if (isUpperCase) {
		value = value.toUpperCase();
	}

	onMount(() => {
		if (initialValue) {
			console.log(initialValue);

			value = initialValue;
		}
	});
</script>

<label for={id} class="svcomp-form-label">
	<div class="label" style={textHelper ? 'margin-bottom: 0px;' : 'margin-bottom: 4px;'}>
		{label}
		<span style="color: #ef4444;">
			{iconRequired ? '*' : ''}
		</span>
	</div>
	{#if textHelper !== ''}
		<div class="text-helper">{textHelper}</div>
	{/if}
	{#if disabled}
		<div class="form-disabled-wrapper">
			<div class="form-disabled">{value ?? placeholder}</div>
		</div>
	{:else}
		<input
			{id}
			class="form {$$props.class}"
			type="text"
			bind:value
			{name}
			{placeholder}
			{disabled}
			{autocomplete}
			maxlength={maxLength}
			on:input={() => {
				dispatch('value', value);
			}}
		/>
		<ErrorMessage {errors} name={nameError} />
	{/if}
</label>
