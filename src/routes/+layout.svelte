
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

<nav class="text-center m-4">
    <a href="/"> TodoList </a>|
    <a href="/storetodo"> Store Todo </a>|
    <a href="/search"> Search </a>
</nav>

<slot></slot>