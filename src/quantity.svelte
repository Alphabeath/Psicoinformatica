<script>

import Eye from "./eyes.svelte";
export let n = 5;

export let mode = "dice"
</script>
{#if mode == "eye"}<Eye n={n}>
</Eye>
{:else} {n}
{/if}