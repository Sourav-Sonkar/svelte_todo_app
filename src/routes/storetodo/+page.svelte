<script>
    // @ts-nocheck

    import { onMount } from "svelte";

    let todos = [];
    let title = "";
    let description = "";
    let dueDate = "";
    onMount(() => {
        todos = localStorage.getItem("todos")
            ? JSON.parse(localStorage.getItem("todos"))
            : [];
    });

    function storeTodo() {
        if (title === "" || description === "" || dueDate === "") {
            alert("Please fill all the fields");
            return;
        }
        let todo = {
            id: new Date().getTime().toString(36),
            title: title,
            description: description,
            dueDate: dueDate,
            completed: false,
        };
        todos.push(todo);
        localStorage.setItem("todos", JSON.stringify(todos));
        title = "";
        description = "";
        dueDate = "";
        window.location.href = "/";
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
    <h1>Store Todo</h1>
    <form on:submit={storeTodo}>
        <div class="form-group m-2">
            <input
                type="text"
                id="title"
                bind:value={title}
                class="form-control"
                placeholder="Enter title"
            />
        </div>
        <div class="form-group m-2">
            <textarea
                class="form-control"
                id="description"
                bind:value={description}
                placeholder="Enter description"
            />
        </div>
        <div class="form-group m-2">
            <input
                type="date"
                id="dueDate"
                bind:value={dueDate}
                class="form-control"
            />
        </div>

        <button type="submit" class="btn btn-primary m-4">Store</button>
    </form>
</div>
