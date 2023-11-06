<!-- Draws a dice face with values from 0 to 9 -->
<script>
export let n = 5;
export let base_color_face="white";
export let base_color_dot="black";
export let bg_opacity=.9;
export let width = 130;
export let height = 130;
</script>

<svg width={width} height={height}>
  <rect x="5" y="5" rx="20" ry="20" width="150" height="150" fill={base_color_face} fill-opacity={bg_opacity}/>
	{#if n == 3}
	    <text x=25 y=130 class="heavy" style="fill: {base_color_dot}; font-size: 35px; user-select:none">{"Nueve"}</text>
	{:else if n == 2}
		  <text x=25 y=130 class="heavy" style="fill: {base_color_dot}; font-size: 35px; user-select:none">{"Ocho"}</text>
	{:else if n == 3}
		  <text x=25 y=130 class="heavy" style="fill: {base_color_dot}; font-size: 35px; user-select:none">{"Siete"}</text>
	{/if}
</svg>
<style>
	rect{
 stroke:black;
stroke-width:5;
		opacity:.9;
	}
</style>