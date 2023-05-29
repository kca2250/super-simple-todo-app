<script lang="ts">
	let newTodo = '';
	let todos: { id: number; text: string }[] = [];
	function addTodo() {
		if (newTodo) {
			todos = [...todos, { id: Date.now(), text: newTodo }];
			newTodo = '';
		}
	}
	function deleteTodo(id: number) {
		todos = todos.filter((todo) => todo.id !== id);
	}
</script>

<div>
	<input
		bind:value={newTodo}
		placeholder="New task"
		on:keydown={(e) => e.key === 'Enter' && addTodo()}
	/>
	<button on:click={addTodo}>Add task</button>
</div>
<ul>
	{#each todos as todo (todo.id)}
		<li>
			{todo.text}
			<button on:click={() => deleteTodo(todo.id)}>Delete</button>
		</li>
	{/each}
</ul>
