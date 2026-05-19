<script>
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
			2rem system-ui,
			"Segoe UI",
			Oxygen,
			"Open Sans",
			sans-serif;
	}
	h1 {
		font-size: 2em;
	}
	input {
		font-size: 1em;
		padding: 1rem 2rem;
		border-radius: 16px;
	}
	li {
		display: grid;
		grid-template-columns: 2rem 1fr;
		gap: 8px;
		padding: 8px;
		list-style-type: none;

		animation-name: slide-in;
		animation-duration: 500ms;
	}
	button {
		border-radius: 16px;
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
