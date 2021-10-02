<script lang="ts">
	import type { ITodo } from './models/ITodo';
	import { onMount } from 'svelte'
	import Card from './components/Card.svelte';

	const storageKey: string = 'svelteTodoExample'
	let todos: ITodo[] = []

	onMount(() => {
		const fromState: string = localStorage.getItem(storageKey)
		const fromStateParsed: ITodo[] = !!fromState
			? JSON.parse(fromState)
			: []
		todos = fromStateParsed
	})

	function handleCreateTodo (todo: string): void {
		const newTodo: ITodo = {
			id: new Date().getTime(),
			todo,
			completed: false,
		}

		todos = [...todos, newTodo];
		setState(todos);
	}

	function handleDeleteTodo (todoId: number): void {
		const todoIndex = todos.findIndex(({ id }) => id === todoId);
		if (todoIndex === undefined) return;
		console.log(`will remove todo at ${todoIndex}`)
		todos.splice(todoIndex, 1)
		todos = [...todos]
		setState(todos)
	}

	function handleCompleteTodo (todoId: number): void {
		const todoIndex = todos.findIndex(({ id }) => id === todoId);
		if (!todoIndex === undefined) return;
		let { id, todo, completed } = todos[todoIndex];
		const updatedTodo = {
			id,
			todo,
			completed: !completed,
		}
		todos.splice(todoIndex, 1, updatedTodo);
		todos = [...todos];
		setState(todos);
	}

	function setState (todos: ITodo[]): void {
		localStorage.setItem(storageKey, JSON.stringify(todos));
	}
</script>

<main>
	<Card
		bind:todos
		on:createTodo={({ detail }) => handleCreateTodo(detail)}
		on:deleteTodo={({ detail }) => handleDeleteTodo(detail)}
		on:completeTodo={({ detail }) => handleCompleteTodo(detail)}
	/>
</main>

<style>
	main {
		display: grid;
		place-items: center;
		width: 100%;
		height: 100%;
		margin: 0;
		padding: 0;
		background: linear-gradient(
			to bottom left,
			#B2E85C,
			#BD981D
		);
	}
</style>