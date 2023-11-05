<!-- Draws a disk of radius proportional to n, for values of n from 0 to 9 -->
<script>
export let n = 5;
export let base_color_face="white";
export let base_color_dot="black";
export let bg_opacity=.9;
export let width = 160;
export let height = 160;
let radius = (width/2-10)*n /9;
</script>
<svg width={width} height={height}>
  <rect x="5" y="5" rx="20" ry="20" width={width-10} height={height-10} fill={base_color_face} fill-opacity={bg_opacity}/>
	<circle cx="75" cy="75" r={radius} fill={base_color_dot} />		
</svg>
<style>
	rect{
   stroke:black;
   stroke-width:5;
	}
	circle{
   stroke:none;
   stroke-width:0;
</style>