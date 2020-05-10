<script>
    export let space = '';
    export let winner;

    $: won = space === winner;
</script>

<div class:winner={won} on:click class="space">{space}</div>

<style>
    .space {
        border: 1px solid gray;
        height: 125px;
        width: 125px;
        flex: 1;
        align-content: center;
        justify-content: center;
        font-size: 75px;
        text-align: center;
        line-height: 125px;
        cursor: pointer;
    }

    .winner {
        color: #26a69a;
    }
</style>
