<script>
    import { fly, scale, slide } from "svelte/transition";
    import { cubicInOut } from "svelte/easing";
    import { onMount } from "svelte";

    let awaitStart = $state(false);
    onMount(() => {
        setTimeout(() => {
            awaitStart = true;
        }, 100);
    })

    let fundraisers = [];
    onMount(function() {
        for (i = 0; i < localStorage.length; i++) {
            if (localStorage.key(i).startsWith("fundraiser-")) {
                let data = JSON.parse(localStorage.getItem(localStorage.key(i)));
                fundraisers.push(data[0] + " for " + data[1]);
            }
        }
    })
</script>
<svelte:head>
    <title>Verkoper | Create Fundraiser</title>
</svelte:head>
<style>
    h1 {
        font-size: 40px;
        font-weight: 800;
    }


    #header {
        position: absolute;
        top: 0;
        left: 30%;
        right: 30%;
        height: 150px;
        background-color: rgb(68, 12, 61);
        border-bottom-right-radius: 20px;
        border-bottom-left-radius: 20px;
        color: white;
    }
</style>
<div id="header" transition:fly={{ y: -200, duration: 800, easing: cubicInOut }}>
    <h1>SETUP FUNDRAISER</h1>
    <h3>Configuration wizard to set up your fundraiser kiosk</h3>
</div>

<div style="height: 160px;"></div>
{#if awaitStart}
    <h2 transition:scale={{delay: 1000, ease:cubicInOut}}>Fill in the details for your new fundraiser</h2>
    <br>
{/if}
{#if awaitStart}
    <div transition:fly={{ easing: cubicInOut, y: 50, duration: 1000, delay: 1300 }}>
        <h3><button id="new-fundraiser" onclick={() => {window.location.href = "/setup/new"}}><span style:font-size="35px" style:transform="translateY(2px)"class="material-symbols-outlined">add_circle</span></button></h3>
        {#each fundraisers as fundraiser}
            console.log(fundraiser);
        {/each}
        {#if fundraisers.length === 0}
            <h4>No fundraisers found. Create a new one to get started!</h4>
        {/if}
    </div>
{/if}

