<script lang="ts">
	import { createEventDispatcher } from "svelte";
	import BaseButton from "./BaseButton.svelte";

	const addTodo = createEventDispatcher();
	let value = '';
	let input: HTMLInputElement;

	function createNewTodo (): void {
		if (!value) return
		addTodo('createTodo', value);
		value = ''
		input.focus()
	}

	function handleKeyup ({ key }: KeyboardEvent): void {
		if (key !== 'Enter') return;
		createNewTodo();
	}
</script>

<section class="add-todo">
	<input
		type="text"
		name="todoInput"
		id="todoInput"
		placeholder="Add a ToDo..."
		class="add-todo__input"
		bind:value
		bind:this={input}
		on:keyup={(ev) => handleKeyup(ev)}
	>
	<BaseButton on:click="{createNewTodo}">
		Add ToDo
	</BaseButton>
</section>

<style>
	.add-todo {
		display: grid;
		grid-template: auto / 1fr max-content;
		gap: 16px;
		align-items: center;
		width: 100%;
		margin-bottom: 16px;
	}

	.add-todo__input {
		height: 48px;
		margin: 0;
		font-size: 18px;
	}
</style>
