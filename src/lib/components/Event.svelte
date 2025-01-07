<script>
    import { fade, fly } from "svelte/transition";
    export let isEvent;
</script>

<div class="event show" in:fly={{ y: -400, duration: 1000 }} out:fade>
    <p>NETPLIX 강렬한 운명의 드라마, 경기크리처</p>
    <button
        onclick={() => {
            isEvent = false;
        }}>X</button
    >
</div>

<style>
    .event {
        width: 100%;
        background-color: #666;
        padding: 5px 1em;
        display: flex;
        justify-content: space-between;
        align-items: center;
        color: white;
        text-align: center;
        margin-bottom: 1em;

        /* 창이 보이지 않게 */
        max-height: 0;
        opacity: 0;
        overflow: hidden;
        transition: all 0.4s;
    }

    /* 기본 : 창이 보이게 */
    .show {
        opacity: 1;
        max-height: 100px;
    }
    .event button {
        padding: 2px;
    }
</style>
