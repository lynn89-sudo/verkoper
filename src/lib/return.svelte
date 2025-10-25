<script>
    import { base } from "$app/paths";

    let prop = $props();
    function goBack() {
        let goTo = base + "/" + prop.source;
        window.location.href = goTo;
    }
</script>

<style>
    div {
        position: fixed;
        top: 20px;
        left: 20px;
        cursor: pointer;
        color: rgb(245, 241, 244);
    }
    span {
        font-size: 40px;
        border-radius: 50%;
        transform: translateY(2.5px);
    }
    button {
        padding: 10px;
    }
</style>
<div>
    <button onclick = {() => {goBack()}}><span class="material-symbols-outlined">arrow_circle_left</span></button>
</div>