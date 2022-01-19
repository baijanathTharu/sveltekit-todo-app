<script lang="ts">
	let todo: string;
	let todos: Array<{ title: string; completed: boolean }> = [
		{ title: 'feed the fish', completed: false }
	];

	function addTodo(e) {
		e.preventDefault();
		todos.unshift({ title: todo, completed: false });
		todos = todos;
		todo = '';
	}

	function toggleTodo(index) {
		todos[index].completed = !todos[index].completed;
		todos = todos;
	}

	function deleteTodo(index) {
		todos.splice(index, 1);
		todos = todos;
	}
</script>

<div class="p-10 text-fuchsia-100">
	<h1 class="text-center text-3xl font-bold">Todo App</h1>

	<div class="flex justify-center my-10">
		<form class="flex flex-col text-xl w-3/4" on:submit={addTodo}>
			<input
				bind:value={todo}
				class="border rounded-sm h-20 px-5 text-black focus:outline-none"
				type="text"
				id="todo"
				placeholder="todo"
				name="todo"
			/>
			<button
				type="submit"
				disabled={!todo}
				class:disabled={!todo}
				class="my-5 bg-slate-600 px-5 py-5 focus:outline-none focus:border-2 focus:border-white"
				>Add Todo</button
			>
		</form>
	</div>

	<div class="flex my-10 w-3/4 mx-auto">
		<ul class="text-xl w-full">
			{#each todos as todo, index}
				<li
					class={`flex items-center my-5 border-2 rounded w-full px-5 ${
						todo.completed ? 'border-red-400' : 'border-fuchsia-50'
					}`}
				>
					<span
						class={`flex-1 text-xl text-fuchsia-100 ${
							todo.completed && 'line-through'
						} cursor-pointer`}
						on:click={() => toggleTodo(index)}
					>
						{todo.title}
					</span>
					<button class="my-5 bg-red-600 rounded px-5 py-2" on:click={() => deleteTodo(index)}
						>Delete</button
					>
				</li>
			{/each}
		</ul>
	</div>
</div>

<style>
	.disabled {
		@apply bg-slate-400 text-slate-900 rounded;
	}
</style>
