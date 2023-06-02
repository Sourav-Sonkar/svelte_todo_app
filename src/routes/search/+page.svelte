<script>
    // @ts-nocheck

    import { onMount } from "svelte";

    /**
     * @type {any[]}
     */
    let filteredTodos = [];
    let search = "";
    let todos = [];

    onMount(() => {
        todos = localStorage.getItem("todos")
            ? JSON.parse(localStorage.getItem("todos"))
            : [];
    });
    function searchTodos() {
        filteredTodos = todos.filter((todo) =>
            todo.title.toLowerCase().includes(search.toLowerCase())
        );
    }
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
    <div class="input-group rounded">
        <input
            type="search"
            bind:value={search}
            class="form-control rounded"
            placeholder="Search"
            aria-label="Search"
            aria-describedby="search-addon"
        />
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <span
            class="input-group-text border-0"
            id="search-addon"
            on:click={searchTodos}
        >
            <i class="fas fa-search" />
        </span>
    </div>

    <ul class="list-group m-2">
        {#each filteredTodos as todo}
            <li class="list-group-item">
                <a href={"/storetodo/" + todo.id}>{todo.title}</a>
            </li>
        {/each}
    </ul>
</div>
