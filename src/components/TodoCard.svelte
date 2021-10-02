<script lang="ts">
import { createEventDispatcher } from "svelte";

	import type { ITodo } from "../models/ITodo";

	export let todo!: ITodo;
	const deleteTodo = createEventDispatcher();
	const completeTodo = createEventDispatcher();

	function handleDelete (): void {
		deleteTodo('deleteTodo', todo.id);
	}

	function handleComplete (): void {
		completeTodo('completeTodo', todo.id);
	}
</script>

<section
	class="todo"
	class:m--completed={todo.completed}
	on:click={handleComplete}
>
	<p
		class="todo__text"
		class:m--completed={todo.completed}
	>{todo.todo}</p>
	<button
		class="todo__delete"
		on:click|stopPropagation={handleDelete}
	>
		Delete
	</button>
</section>

<style>
	p {
		all: unset;
	}

	.todo {
		cursor: pointer;
		display: grid;
		grid-template: auto / 1fr max-content;
		align-items: center;
		justify-content: start;
		min-height: 56px;
		margin-top: 8px;
		border-radius: 4px;
		padding: 8px;
		background: #f1f2f4;
		font-size: 16px;
		letter-spacing: 1px;
	}

	.todo.m--completed {
		background: #e7e7e7;
	}

	.todo__text.m--completed {
		text-decoration: line-through;
	}

	.todo__delete {
		all: unset;
		cursor: pointer;
		color: #cc4c40;
		font-size: 10px;
	}
</style>
