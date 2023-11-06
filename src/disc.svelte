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
     <text x=25 y=130 class="heavy" style="fill: {"black"}; font-size: 35px; user-select:none">{"Nueve"}</text>
<style>
	rect{
   stroke:black;
   stroke-width:5;
	}
</style>