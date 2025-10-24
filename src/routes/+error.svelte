<script>
    import { base } from "$app/paths";
    import { onMount } from "svelte";
    let countdown = $state(5);

    let criticalError = $state(false);

    onMount(function() {
        setInterval(() => {
            if (countdown > 0 && !criticalError) {
                countdown -= 1;
            }
        }, 1000);

        if (sessionStorage.getItem("redirected_from_error") === "true") {
            criticalError = true;
        }
    })

    $effect(function() {
        if (countdown === 0) {
            sessionStorage.setItem("redirected_from_error", "true");
            window.location.href = "/";
        }
    })
    
</script>
<svelte:head>
    <title>Verkoper | Error Screen</title>
</svelte:head>
<style>
    h1, h3 {
        font-family: Montserrat;
    }
    h2 span {
        font-family: Space Grotesk, Montserrat;
        background-color: rgb(53, 9, 53);
        color: white;
        padding: 15px;
        border-radius: 30px;
    }
    button {
        background-color: #38002f;
        color: white;
        border: none;
        padding: 15px 30px;
        border-radius: 30px;
        font-size: 1.2em;
        cursor: pointer;
        transition: all 0.3s ease-in-out;
        font-family: Space Grotesk, Montserrat;
        text-align: center;
    }
    button:hover {
        background-color: #721062;
        transform: scale(1.05);
    }
</style>
<h1>Uh oh :(</h1>
<h3>Something went wrong.</h3>
<br>
{#if !criticalError}
    <h2>We'll try to restart the app in <span>{countdown}</span></h2>
{:else}
    <h2>We're not quite sure what the error is. Check back in on Verkoper in a bit!</h2>
    <br>
    <h3><button onclick={function() { window.location.href = "/"}}>Retry</button></h3>
{/if}
<br><br>
<h3>Verkoper | Web-Based Kiosk System powered by Svelte</h3>