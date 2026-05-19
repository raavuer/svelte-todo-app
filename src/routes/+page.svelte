<script lang="ts">
	import { onMount } from "svelte";

	let todos = $state([]);
	onMount(() => {
		todos = JSON.parse(localStorage.getItem("todos") ?? "[]");
	});

	function addTodo() {
		const todo = this.value;
		if (todo === "" || todos.includes(todo)) return;
		todos.push(todo);
		localStorage.setItem("todos", JSON.stringify(todos));
		this.value = "";
	}
	function removeTodo() {
		const index = this.parentElement.id.slice(0, 1);
		todos.splice(index, 1);
		localStorage.setItem("todos", JSON.stringify(todos));
	}
</script>

<main>
	<h1>Todo List</h1>

	<input type="text" onchange={addTodo} />

	<ul>
		{#each todos as todo, index (todo)}
			<li id={index + "-" + todo}>
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

		font:
			1.5rem system-ui,
			"Segoe UI",
			Oxygen,
			"Open Sans",
			sans-serif;
	}
	input {
		font-size: 1em;
		padding: 1rem;
		border-radius: 1em;
	}
	li {
		display: grid;
		grid-template-columns: 2rem 1fr;
		align-content: space-between;
		gap: 8px;
		padding: 8px;
		list-style-type: none;

		animation-name: slide-in;
		animation-delay: calc(250ms * sibling-index());
		animation-duration: 500ms;
	}
	li:hover > span {
		text-decoration: underline;
	}
	button {
		border-radius: 16px;
	}
	button:hover {
		border-color: maroon;
		background-color: crimson;
	}
	@keyframes slide-in {
		from {
			translate: 100% 0;
			opacity: 0;
		}
		to {
			translate: 0 0;
			opacity: 1;
		}
	}
</style>
