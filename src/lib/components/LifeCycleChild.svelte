<script>
    import { onMount, afterUpdate, onDestroy } from "svelte";

    // 컴포넌트가 제거될 때 사용
    onDestroy(() => {
        console.log("onDestroy");
    });
</script>

<main>
    <h1>child</h1>
</main>
