<script lang="ts">
	export let type = 'button';
</script>

<button
	type={type}
	class="base-button"
	on:click
>
	<slot>Enter some text</slot>
</button>

<style>
	.base-button {
		all: unset;
		cursor: pointer;
		display: grid;
		place-items: center;
		height: 48px;
		border-radius: 2px;
		padding: 0 16px;
		background: rgb(15, 255, 235);
		font-size: 18px;
		font-weight: 600;
		letter-spacing: 1px;
		color: #333;
	}
</style>
