<script>
    import { onMount } from "svelte";
    import { cubicIn, cubicInOut } from "svelte/easing";
    import {fly, slide} from "svelte/transition";
    import { base } from "$app/paths";

    let active = false;
    onMount(() => {
        setTimeout(() => {
            active = true;
        }, 100);
    });
</script>
<svelte:head>
    <title>Verkoper | Main Menu</title>
</svelte:head>
<style>
    @keyframes anim {
        0% {
            transform: translateY(0) rotate(0deg);
        }
        50% {
            transform: translateY(-5px) rotate(1deg);
        }
        100% {
            transform: translateY(0);
        }
    }
    #verk {
        color: #721062;
        transform: scale(1.2);
        opacity: 1;
        user-select: none;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
    }
    #verk span {
        display: inline-block;
        animation: anim 1.5s ease-in-out infinite;
    }
    #verk span:nth-child(1) { animation-delay: 0s; }
    #verk span:nth-child(2) { animation-delay: 0.1s; }
    #verk span:nth-child(3) { animation-delay: 0.2s; }
    #verk span:nth-child(4) { animation-delay: 0.3s; }
    #verk span:nth-child(5) { animation-delay: 0.4s; }
    #verk span:nth-child(6) { animation-delay: 0.5s; }
    #verk span:nth-child(7) { animation-delay: 0.6s; }
    #verk span:nth-child(8) { animation-delay: 0.7s; }

    #verk-caption {
        opacity: 1;

        span {
            background-color: rgb(113, 68, 134);
            color: white;
            padding: 15px;
            border-radius: 30px;
            transition: all 0.3s ease-in-out;
        }
    }
    #menu {
        margin-top: 30px;
        font-family: Space Grotesk, Montserrat;
        text-align: center;
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
        }
        button:hover {
            background-color: #721062;
            transform: scale(1.05);
        }
    }
</style>
<h1 id="verk"><span>v</span><span>e</span><span>r</span><span>k</span><span>o</span><span>p</span><span>e</span><span>r</span></h1>
{#if active}
    <h2 id="verk-caption"><span transition:slide={{delay:200, duration: 1200, easing: cubicInOut}}>Web-Based Kiosk System powered by Svelte</span></h2>
    <br>

    <div id="menu" transition:fly={{ easing: cubicInOut, y: 50, duration: 1000, delay: 1100 }}>
        <a href="{base}/kiosk"><button>Kiosk Mode</button></a><br><br>
        <a href="{base}/setup"><button>Setup Mode</button></a>
    </div>
{/if}
