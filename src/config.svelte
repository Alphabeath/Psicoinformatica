<script>
  import Quantity from "./quantity.svelte";
	import {enterInLocalLog} from "./log.js";
	import {dateInOrgmodeFormat} from "./log.js";	
	// Parameters	
  export let log={}
	export let params={};
  // Variables
  let modes = ["dice", "heap", "rect", "disc"];
  let colors = ["white", "black", "green", "yellow", "red", "blue"];
  let opacities = [.1,.2,.3,.4,.5,.6,.7,.8,.9];
  let i = 3;
  let maxValue = 9;
  let valuesMenu = [0,1,2,3,4,5,6,7,8,9];	
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
	input[type='text']{width:100%}
</style>

<h1 align="center">Configuration</h1>

<h2>Logs</h2> 
<!-- <input type=checkbox bind:checked={params.logInteractions}> -->
{#if params.logInteractions}
<ul>
<li><label>Learner's name: <input bind:value={params.learner} placeholder={params.learner}></label>
<li><label>Instructor's name: <input bind:value={params.teacher} placeholder={params.teacher}></label>
<li>DOWNLOAD the log in 
	<button><a download="{fileName()}.txt" href="{URL.createObjectURL(log.text)}" id="downloadLinkTEXT">TEXT</a></button> or 
  <button><a download="{fileName()}.csv" href="{URL.createObjectURL(log.csv)}" id="downloadLinkCSV">CSV</a></button> format.
<li> <button on:click={resetLogs}>RESET the log</button></li>
</ul>
	<!--
<label>
 <input type=checkbox bind:checked={params.activeServer}> Automatic log to server 
  <input type='text' disabled={!params.activeServer} bind:value={params.server} placeholder={params.server}>
</label>
-->
<!--
Statistics: (<a download="stats.csv" href="{URL.createObjectURL(log.blob)}" id="downloadLink">Download local log</a>
-->
{/if}

<h2>Apparences</h2>
<table>
	<tr><td>
		
<h3>Mode = {params.mode}</h3>
		{#each modes as mode }
		<input type=radio bind:group={params.mode} value={mode}> {mode}
		{/each}
		
		
<h3>Set of Values = [{params.values.sort()}]</h3>
{#each valuesMenu as v}
		<input type=checkbox bind:group={params.values} value={v}
					 disabled={v>maxValue} 
					 >{v}
{/each}

<h3>Colors: {params.fg} on {params.bg} </h3>
<div>Foreground:
	<!--suggestion jo ? 	<input type="color"/> -->
	{#each colors as color}
	<input type=radio bind:group={params.fg} value={color}> {color}
	{/each}
</div>
<div>Background:
	{#each colors as color}
	<input type=radio bind:group={params.bg} value={color}> {color}
	{/each}
</div>
		<label>Background Opacity: {params.bg_opacity} 
	<input 
				 type=range 
				 bind:value={params.bg_opacity} 
				 min=0.01 max=0.99 step=0.01
				 on:input={switchOnRedraw}
				 >
		</label>
		
</td>
<td>
<h3>Example for n={params.values[i]}</h3>

<label align=center>
	<input 
				 type=range 
				 bind:value={i} 
				 min=0 max={params.values.length-1}
				 on:input={switchOnRedraw}
				 >
	<center>
		{#if redraw}
	<Quantity n={params.values[i]} 
						mode={params.mode}
						fg={params.fg}
						bg={params.bg}												  
						bg_opacity={params.bg_opacity}
						></Quantity>
		{switchOffRedraw()}
		{:else}
	<Quantity n={params.values[i]} 
						mode={params.mode}
						fg={params.fg}
						bg={params.bg}
						bg_opacity={params.bg_opacity}
						></Quantity>
		{/if}
	</center>
</label>
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
	
	<h2><input type=checkbox bind:checked={params.visualFeedback}> Visual Feedback </h2>
{#if params.visualFeedback}
<label>"Correct" visual feedback: <input disabled={!params.visualFeedback} type="text" bind:value={params.visualFeedbackCorrect} placeholder={params.visualFeedbackCorrect}></label>
<label>"Incorrect" visual feedback: <input disabled={!params.visualFeedback} type="text" bind:value={params.visualFeedbackInCorrect} placeholder={params.visualFeedbackInCorrect}></label>
<label>"Excellent" visual feedback: <input disabled={!(params.visualFeedback&params.gameFeatures)} type="text" bind:value={params.visualFeedbackExcellent} placeholder={params.visualFeedbackExcellent}></label>
<label>"Pass" visual feedback: <input disabled={!(params.visualFeedback&params.gameFeatures)} type="text" bind:value={params.visualFeedbackPass} placeholder={params.visualFeedbackPass}></label>
<label>"Fail" visual feedback: <input disabled={!(params.visualFeedback&params.gameFeatures)} type="text" bind:value={params.visualFeedbackFail} placeholder={params.visualFeedbackFail}></label>
{/if}

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

<h2><input type=checkbox bind:checked={params.playSound}> Sounds</h2>
{#if params.playSound}
<label>"Correct" Exercise sound URL: <input disabled={!params.playSound} type="text" bind:value={params.correctSoundURL} placeholder={params.correctSoundURL}></label>
<label>"Incorrect" Exercise sound URL: <input disabled={!params.playSound} type="text" bind:value={params.incorrectSoundURL} placeholder={params.incorrectSoundURL}></label>
<label>"Fail" Game sound URL: <input disabled={!params.playSound} type="text" bind:value={params.gameSoundsURLs.fail} placeholder={params.gameSoundsURLs.fail}></label>
<label>"Pass" Game sound URL: <input disabled={!params.playSound} type="text" bind:value={params.gameSoundsURLs.pass} placeholder={params.gameSoundsURLs.pass}></label>
<label>"Excel" Game sound URL: <input disabled={!params.playSound} type="text" bind:value={params.gameSoundsURLs.excel} placeholder={params.gameSoundsURLs.excel}></label>
{/if}

