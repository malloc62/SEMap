<style>
    :global(:root) {
        --light-1: rgb(255,255,255);
        --light-2: rgb(228,230,232);
        --light-3: rgb(208,210,212);

        --dark-1: rgb(0,0,0);
        --dark-2: rgb(18,20,22);
        --dark-3: rgb(38,40,42);

        font-family: 'Open Sans', sans-serif, serif;
        font-size: 1.0rem;
    }

    body {
        display: flex;

        padding: 0;
        margin: 0;

        height: 100vh;
        width: 100vw;

        overflow: hidden;

        color: var(--dark-1);

        background: var(--light-1);
    }
</style>

<body>
    <slot />
</body>
