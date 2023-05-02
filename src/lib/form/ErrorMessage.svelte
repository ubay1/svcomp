<script lang="ts">
	export let name: string = '';
	export let nameConfirm: string = '';
	export let min: number = 0;
	export let errors: string[] = [];

	function checkTypeError(type: string): string {
		let result: string = '';
		switch (type) {
			case 'required':
				result = `${name} wajib diisi.`;
				break;
			case 'min':
				result = `${name} minimal memiliki ${min} karakter.`;
				break;
			case 'only_number':
				result = `${name} Hanya bisa angka.`;
				break;
			case 'match_field':
				result = `${name} harus sama dengan ${nameConfirm}.`;
				break;

			default:
				break;
		}

		return result;
	}
</script>

<div class="container-error-msg">
	{#each errors as error}
		<div class="label">
			{checkTypeError(error)}
		</div>
	{/each}
</div>

<style scoped>
	.container-error-msg {
		display: flex;
		flex-direction: column;
	}
	.container-error-msg .label {
		font-size: 0.75rem;
		line-height: 1rem;
		color: #ef4444;
	}
</style>
