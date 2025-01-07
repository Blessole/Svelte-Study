<script>
    import { onMount, afterUpdate } from "svelte";
    import LifeCycleChild from "./LifeCycleChild.svelte";
    let count = 0;
    let isShow = true;
    // 컴포넌트가 Dom에 추가되기 전 실행
    onMount(() => {
        console.log("onMount");
    });

    // 컴포넌트가 업데이트된 후 실행
    afterUpdate(() => {
        console.log("afterUpdate");
    });
</script>

{#if isShow}
    <LifeCycleChild />
{/if}

<button onclick={() => (isShow = false)}>Child 제거</button>
<button onclick={() => (count += 1)}>{count}교시</button>
