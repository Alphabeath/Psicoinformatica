<!-- Draws a container filled up to n, where n is from 0 to 9 -->
<script>
export let n = 5;
export let base_color_face="white";
export let base_color_dot="black";
export let bg_opacity=.9;
export let width = 160;
export let height = 160;
let heightFilled = (height-10)*n /9;
</script>
<svg width={width} height={height}>
  <rect x="5" y="5" 
				width={width-10} height={height-10}
				style="fill:{base_color_face};fill-opacity:{bg_opacity};stroke-width:10;stroke:black"
				/>
	<rect x="10" y={height-heightFilled} 
				width={width-20} height={heightFilled-10}
				style="fill:{base_color_dot};stroke-width:0;stroke:{base_color_dot}"
				/>
</svg>

<style>
	rect{
    stroke:black;
    stroke-width:5;
		rx:0; 
		ry:0;
	}
</style>