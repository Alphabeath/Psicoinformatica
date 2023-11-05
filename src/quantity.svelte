<script>
import Dice from "./dice.svelte";
import Heap from "./heap.svelte";
import Disc from "./disc.svelte";
import Rect from "./rect.svelte";
export let n = 5;
export let bg="white";
export let fg="black";
export let bg_opacity=.9;
export let width = 160;
export let height = 160;
export let mode = "dice"
</script>
{#if mode == "dice"}<Dice n={n}
													base_color_face={bg} 
													base_color_dot={fg}
												  bg_opacity={bg_opacity}
													width = {width}
													height= {height}
													></Dice>
{:else if mode == "heap"}<Heap n={n}
													base_color_face={bg} 
													base_color_dot={fg}
												  bg_opacity={bg_opacity}
													width = {width}
													height= {height}
													></Heap> 
{:else if mode == "disc"}<Disc n={n}
													base_color_face={bg} 
													base_color_dot={fg}
												  bg_opacity={bg_opacity}
													width = {width}
													height= {height}
													></Disc>
{:else if mode == "rect"}<Rect n={n}
													base_color_face={bg} 
													base_color_dot={fg}
												  bg_opacity={bg_opacity}
													width = {width}
													height= {height}
													></Rect>
{:else} {n}
{/if}