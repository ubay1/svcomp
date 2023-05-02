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

<style>
	/* https://nekocalc.com/px-to-rem-converter */

	.svcomp-form-label {
		position: relative;
		width: 100%;
	}

	.svcomp-form-label .label {
		color: black;
		font-size: 0.875rem;
		line-height: 1.25rem;
		font-weight: 500;
	}

	.svcomp-form-label .text-helper {
		font-size: 0.75rem;
		line-height: 1rem;
		color: #9ca3af;
		margin-bottom: 0.25rem;
		font-style: italic;
	}

	.svcomp-form-label .form {
		background-color: white;
		padding-left: 0.75rem;
		padding-right: 0.75rem;
		height: 2.5rem;
		border-radius: 0.25rem;
		width: -webkit-fill-available;
		font-size: 0.875rem;
		line-height: 1.25rem;
		border: 1px solid #9ca3af;
	}
	.svcomp-form-label .form:focus {
		outline: none;
		border-color: black;
	}

	.svcomp-form-label .form-disabled-wrapper {
		display: flex;
		width: 100%;
		justify-content: space-between;
		align-items: center;
	}
	.svcomp-form-label .form-disabled {
		background-color: #d1d5db;
		color: #353535;
		padding: 0.75rem;
		border-radius: 0.25rem;
		width: -webkit-fill-available;
		font-size: 0.875rem;
		line-height: 1.25rem;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
</style>
