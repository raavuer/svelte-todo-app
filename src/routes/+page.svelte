<script lang="ts">
	let todos: string[] = $state([]);
</script>

<main>
	<h1>Todo List</h1>

	<input
		type="text"
		onchange={function () {
			todos.push(this.value);
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
