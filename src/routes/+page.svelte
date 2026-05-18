<script lang="ts">
	import { onMount } from "svelte";

	let todos: string[] = $state([]);
  onMount(() => {
    todos = JSON.parse(localStorage.getItem("todos") || "[]");
  });
</script>

<main>
	<h1>Todo List</h1>

	<input
		type="text"
		onchange={function () {
			todos.push(this.value);
      localStorage.setItem("todos", JSON.stringify(todos));
		}}
	/>

	<ul>
		{#each todos as todo (todos.indexOf(todo))}
			<li>{todo}</li>
		{/each}
	</ul>
</main>

<style>
	main {
		display: grid;
		place-items: center;
		font-family: system-ui, 'Segoe UI', Oxygen, 'Open Sans', sans-serif;
	}
</style>
