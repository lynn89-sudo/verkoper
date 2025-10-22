<script>
    import { base } from "$app/paths";
    import { onMount } from "svelte";
    let countdown = $state(5);

    onMount(function() {
        setInterval(() => {
            if (countdown > 0) {
                countdown -= 1;
            }
        }, 1000);
    })

    $effect(function() {
        if (countdown === 0) {
            window.location.href = base;
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
</style>
<h1>Uh oh :(</h1>
<h3>Something went wrong.</h3>
<br>
<h2>We'll redirect you in <span>{countdown}</span></h2>
<br><br>
<h3>verkoper</h3>