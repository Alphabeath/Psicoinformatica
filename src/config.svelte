<script>
  import Quantity from "./quantity.svelte";
	import {enterInLocalLog} from "./log.js";
	import {dateInOrgmodeFormat} from "./log.js";	
	// Parameters	
  export let log={}
	export let params={};
  // Variables
  let modes = ["Poder", "Vulnerable"];
  let colors = ["white", "black"];
  let i = 3;
  let redraw = true;
	
	// Functions
	function resetLogs() {
		console.log("Reseting the logs.");
		log = { 
  		test_number: 0,
	  	time_last_display: 0,
		  text_diary: ["# Date Time (...) "],
		  csv_diary: ["Test no, Test Name, Learner, Trainer, C_0, C_1, C_2, C_3, C_4, Value selected , Correction , Date, Answering Time (ms), Other Parameters"],
		  text: new Blob(["# No test was executed before saving this text log. "], {type: 'text/plain'}),
		  csv: new Blob(["# No test was executed before saving this csv log. "], {type: 'text/csv'})
		};
	}
	function test() {
		console.log("Test Function");
	}
	function fileName() {
		return dateInOrgmodeFormat()+"-InCA-BCT-"+params.learner+" trained by "+params.teacher;
	}
	function switchOffRedraw() {
    redraw = false;
	}
	function switchOnRedraw() {
    redraw = true;
	}
</script>

<style>
	input[type=checkbox],
	input[type=radio]
	{
    transform: scale(2);
			margin-left:30px;
			margin-right:10px;
}
	label{
	margin:10px;
	}
</style>

<h1 align="center">Configuration</h1>

<h2>Logs</h2> 
{#if params.logInteractions}
	<ul>
	<li><label>Learner's name: <input bind:value={params.learner} placeholder={params.learner}></label>
	<li><label>Instructor's name: <input bind:value={params.teacher} placeholder={params.teacher}></label>
	<li>DOWNLOAD the log in 
		<button><a download="{fileName()}.txt" href="{URL.createObjectURL(log.text)}" id="downloadLinkTEXT">TEXT</a></button> or 
	<button><a download="{fileName()}.csv" href="{URL.createObjectURL(log.csv)}" id="downloadLinkCSV">CSV</a></button> format.
	<li> <button on:click={resetLogs}>RESET the log</button></li>
	</ul>
{/if}

<h2>Apparences</h2>
<table>
	<tr><td>
		
<h3>Mode = {params.mode}</h3>
		{#each modes as mode }
		<input type=radio bind:group={params.mode} value={mode}> {mode}
		{/each}
		
		
<h3>Colors: {params.fg} on {params.bg} </h3>
<div>Foreground:
	{#each colors as color}
	<input type=radio bind:group={params.fg} value={color}> {color}
	{/each}
</div>
<div>Background:
	{#each colors as color}
	<input type=radio bind:group={params.bg} value={color}> {color}
	{/each}
</div>		
</td>
</tr>
</table>


<h2>Exercises features</h2>
<label>Nb values to choose from: {params.nbChoices}
	<input type=range bind:value={params.nbChoices} min=1 max=5>
</label>
<label>Waiting Time between exercises: {params.waiting_time} seconds
	<input type=range bind:value={params.waiting_time} min=0 max=10 step=0.1>
</label>
<label>Pressing time to exit game mode: {params.durationHomeButton} seconds
	<input type=range bind:value={params.durationHomeButton} min=0 max=10 step=0.1>
</label>
	

<h2><input type=checkbox bind:checked={params.gameFeatures}> Games features</h2>
{#if params.gameFeatures}
<label>Game Length: {params.gameLength}
	<input type=range bind:value={params.gameLength} min=1 max=50>
</label>
<label>Game Threshold for Excellent: {params.gameThresholds.excel}
	<input type=range bind:value={params.gameThresholds.excel} min={params.gameThresholds.pass} max={params.gameLength}>
</label>
<label>Game Threshold for Pass: {params.gameThresholds.pass}
	<input type=range bind:value={params.gameThresholds.pass} min=1 max={params.gameThresholds.excel}>
</label>
{/if}


