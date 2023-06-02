<script>
	// @ts-nocheck

	import { onMount } from "svelte";

	/**
	 * @type {string | any[]}
	 */
	let todoList = [];
	let isloading = true;

	function setTodos() {
		todoList = localStorage.getItem("todos")
			? JSON.parse(localStorage.getItem("todos"))
			: [];
	}

	function changeStatus(id) {
		todoList.map((todo) => {
			if (todo.id === id) {
				todo.completed = !todo.completed;
			}
		});
		localStorage.setItem("todos", JSON.stringify(todoList));
		setTodos();
	}

	function deleteTodo(id) {
		todoList = todoList.filter((todo) => todo.id !== id);
		localStorage.setItem("todos", JSON.stringify(todoList));
		setTodos();
	}

	onMount(() => {
		setTodos();
		isloading = false;
	});
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css"
	/>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/5.1.1/css/bootstrap.min.css"
	/>
</svelte:head>

<div class="container">
	{#if todoList.length === 0 && !isloading}
		<h1 class="text-center">No Todos Stored</h1>
	{:else}
		<ol class="list-group list-group-numbered">
			{#each todoList as todo}
				<li
					class="list-group-item d-flex justify-content-between align-items-start"
				>
					<div class="ms-2 me-auto">
						<div class="fw-bold text-left">{todo.title}</div>
						Due Date: {todo.dueDate}
					</div>
					{#if todo.completed}
						<span class="badge bg-primary rounded-pill m-2"
							>Completed</span
						>
					{/if}
					{#if !todo.completed}
						<button
							class="btn btn-sm btn-outline-success m-1"
							on:click={() => changeStatus(todo.id)}
						>
							Done
						</button>
					{/if}
					<button
						class="btn btn-sm btn-outline-danger m-1"
						on:click={() => deleteTodo(todo.id)}
					>
						Delete
					</button>
					<a
						class="btn btn-sm btn-outline-primary m-1"
						href={"/storetodo/" + todo.id}
					>
						Edit
					</a>
				</li>
			{/each}
		</ol>
	{/if}
</div>
