<script lang="ts">
	import { onMount } from "svelte";

	let todos: string[] = $state([]);
	onMount(() => {
		todos = JSON.parse(localStorage.getItem("todos") ?? "[]");
	});
</script>

<main>
	<h1>Todo List</h1>

	<input
		type="text"
		onchange={function () {
			const todo = this.value;
			if (todo === "") return;
			todos.push(todo);
			localStorage.setItem("todos", JSON.stringify(todos));
		}}
	/>

	<ul>
		{#each todos as todo, index (index)}
			<li>
				<button
					type="button"
					onclick={function () {
						todos.splice(index, 1);
						localStorage.setItem("todos", JSON.stringify(todos));
					}}>X</button
				>
				{todo}
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
