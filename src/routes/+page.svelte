<script lang="ts">
	import { onMount } from "svelte";

	let todos: string[] = $state([]);
	onMount(() => {
		todos = JSON.parse(localStorage.getItem("todos") ?? "[]");
	});

	function addTodo () {
		const todo = this.value;
		if (todo === "") return;
		todos.push(todo);
		localStorage.setItem("todos", JSON.stringify(todos));
		this.value = "";
	};
	function removeTodo () {
		todos.splice(this.index, 1);
		localStorage.setItem("todos", JSON.stringify(todos));
	};
</script>

<main>
	<h1>Todo List</h1>

	<input type="text" onchange={addTodo} />

	<ul>
		{#each todos as todo, index (index)}
			<li>
				<button type="button" onclick={removeTodo}>X</button>
				<span>{todo}</span>
			</li>
		{/each}
	</ul>
</main>

<style>
	main {
		display: grid;
		place-items: center;
		font-family: system-ui, "Segoe UI", Oxygen, "Open Sans", sans-serif;
	}
	li {
		padding: 0.25rem;
		list-style-type: none;
	}
</style>
