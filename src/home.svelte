<script>
import Quantity from "./quantity.svelte";
export let maxValue = 6;
export let page = "home";
export let params ={};
let rectValue = 1+Math.floor(Math.random()*(maxValue-1));
let diceValue = 1+Math.floor(Math.random()*(maxValue-1));
let heapValue = 1+Math.floor(Math.random()*(maxValue-1));
let discValue = 1+Math.floor(Math.random()*(maxValue-1));
</script>

<h1 align=center>
	InCA-WhatIsMore-PICourse-V1.0
</h1>

<table align="center"><tr>
<td on:click={()=>{params.mode="rect";page="game"}}>
	<Quantity n={rectValue} mode="rect" 
						fg={params.fg}
						bg={params.bg}												  
						bg_opacity={params.bg_opacity}></Quantity></td>
<td on:click={()=>{params.mode="dice";page="game"}}>
	<Quantity n={diceValue} mode="dice" 
						fg={params.fg}
						bg={params.bg}												  
						bg_opacity={params.bg_opacity}></Quantity></td>
<td on:click={()=>{params.mode="heap";page="game"}}>
	<Quantity n={heapValue} mode="heap" 
						fg={params.fg}
						bg={params.bg}												  
						bg_opacity={params.bg_opacity}></Quantity></td>
<td on:click={()=>{params.mode="disc";page="game"}}>
	<Quantity n={discValue} mode="disc" 
						fg={params.fg}
						bg={params.bg}												  
						bg_opacity={params.bg_opacity}></Quantity></td>
</tr>	
</table>

<div ALIGN=RIGHT>
		last edited by <a href="https://barbay.cl">JyBy</a>
</div>
	