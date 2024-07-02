<slot />

<style>
    :global(body) {
        background: linear-gradient(90deg, #f5e9d7, #fedeff);
        background-size: 1000% 1000%;
        animation: gradientAnimation 20s ease infinite;
        margin: 0 auto;
        width: 100%;
        min-height: 100vh;
        font-family: Arial, sans-serif;
    }

    @keyframes gradientAnimation {
        0% {
            background-position: 0% 50%;
        }

        50% {
            background-position: 100% 50%;
        }

        100% {
            background-position: 0% 50%;
        }
    }




</style>
