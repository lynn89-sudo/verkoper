<script>
    import { fly, scale, slide } from "svelte/transition";
    import { cubicInOut } from "svelte/easing";
    import { onMount } from "svelte";
    import { base } from "$app/paths";

    import Return from "$lib/return.svelte";

    let awaitStart = $state(false);

    onMount(() => {
        setTimeout(() => {
            awaitStart = true;
        }, 100);


    });

    let formName = $state("");
    let formClub = $state("");
    let formCurrency = $state("");
    let formId = $state(0);
    function handleSubmit(event) {
       let clock = new Date();
        formId = clock.getTime();

        let data = [
            formName,
            formClub,
            formCurrency,
            [],
            formId
        ]

        localStorage.setItem("fundraiser-" + formId, JSON.stringify(data));
        window.location.href = base + "/setup";
    }
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
<Return source="setup"/>
<div id="header" transition:fly={{ y: -200, duration: 800, easing: cubicInOut }}>
    <h1>SETUP FUNDRAISER</h1>
    <h3>Configuration wizard to set up your fundraiser kiosk</h3>
</div>

<div style="height: 160px;"></div>
{#if awaitStart}
    <h2 transition:scale={{delay: 200, ease:cubicInOut}}>Fill in the details for your new fundraiser</h2>
    <br>
{/if}
{#if awaitStart}
    <div transition:fly={{ easing: cubicInOut, y: 50, duration: 1000, delay: 500 }}>
        <form id="newFundraiser" onsubmit={() => {handleSubmit()}}>
            <label for="fundraiserName">Fundraiser Name:</label><br><br>
            <input bind:value={formName} type="text" id="fundraiserName" placeholder = "Oct. 23 Breakfast Sale" name="fundraiserName" required><br><br>
            <label for="beneficiaryName">Club/Event Name:</label><br><br>
            <input bind:value={formClub} type="text" id="clubName" placeholder = "Coding Café" name="clubName" required><br><br>
            <label for="beneficiaryName">Currency Unit:</label><br><br>
            <input bind:value={formCurrency} type="text" id="currency" name="currency" required placeholder="$"><br><br>
            <button type="submit">Create Fundraiser</button>
        </form>
    </div>
{/if}

