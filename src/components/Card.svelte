<script lang="ts">
	import type { ITodo } from '../models/ITodo';
	import { onMount } from 'svelte';

	import AddTodo from './AddTodo.svelte';
	import TodoCard from './TodoCard.svelte';

	export let todos: ITodo[];

	$: completedTodos = todos.filter(({ completed }) => completed)
	$: incompleteTodos = todos.filter(({ completed }) => !completed)

	onMount(() => {
		console.log('card mounted')
	})
</script>

<section class="card">
	<div
		class="card__entry"
		role="presentation"
	>
		<AddTodo on:createTodo />
	</div>
	<div
		class="card__list-wrapper"
		class:m--no-results={!todos.length}
		role="presentation"
	>
		{#if !todos.length}
			<p class="card__no-results">
				Add a ToDo to get started
			</p>
		{:else}
			{#each incompleteTodos as todo}
				<TodoCard
					bind:todo
					on:deleteTodo
					on:completeTodo
				/>
			{/each}
			{#each completedTodos as todo}
				<TodoCard
					bind:todo
					on:deleteTodo
					on:completeTodo
				/>
			{/each}
		{/if}
	</div>
</section>

<style>
	.card {
		display: grid;
		grid-template: auto 1fr / 1fr;
		height: 350px;
		width: 500px;
		border-radius: 4px;
		padding: 32px 16px;
		background: rgba(25, 25, 25, 0.4);
		box-shadow: 2px 2px 3px rgba(25, 25, 25, 0.4);
	}

	.card__list-wrapper {
		overflow: auto;
	}

	.card__list-wrapper.m--no-results {
		display: grid;
		place-items: center;
	}

	.card__no-results {
		font-size: 24px;
		color: #f1f2f4;
		font-weight: 900;
		letter-spacing: 1px;
	}
</style>
