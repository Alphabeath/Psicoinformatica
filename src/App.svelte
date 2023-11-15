<script>
	// Local variables
	let pressed = false;
	// Imports
	import Home from "./home.svelte";
	import W3Menu from "./w3menu.svelte";
	import Game from "./game.svelte";
	import Config from "./config.svelte";
	import Info from "./info.svelte";	
	import Story from "./story.svelte";
	import Test from "./test.svelte";
	// External Variables
	export let page = "menu";
	export let log ={ 
		test_number: 0,
		time_last_display: 0,
		text_diary: ["# Date Time (...) "],
		csv_diary: ["Test no, Test Name, Learner, Trainer, C_0, C_1, C_2, C_3, C_4, Value selected , Correction , Date, Answering Time (ms), Other Parameters"],
		text: new Blob(["# No test was executed before saving this text log. "], {type: 'text/plain'}),
		csv: new Blob(["# No test was executed before saving this csv log. "], {type: 'text/csv'})
	}
  export let params={
		waiting_time : 1,
		durationHomeButton : 0,
		noMoreBotton : false,
		noMoreSoundURL : "", 
		mode : 'dice',
	  	randomMode: false,
		randomModes: false,		modes : ["dice","heap"],
		randomColors:false, colors : ["black","red","blue"],
		randomOpacity:false, opacities : [.2,.3,.5,.7,.9],
		nbChoices : 2,
		bg : "black",
		fg : "green",
		bg_opacity:".2",
		values : [1,2,3,4,5,6],
		playSound : false,
		visualFeedback: true,
		gameFeatures : true,
   	 	gameLength : 5,
		gameThresholds : {pass:.5, excel:.9},
		gameWaitingTimeForResultInMiliseconds: 2000,
		logInteractions : true,
		server : "https://buho.dcc.uchile.cl/~inca-bct/log.php",
		activeServer: false,
		learner: "unnamed",
		teacher: "unnamed",
		historia: 1,
		correctAnswer:  ["jugueton", "trastorno", "deseoso", "insitencia", "preocupacion"],
		AnswerEyes: [
		["jugueton", "reconfortante", "irritado", "aburrido"], 
		["aterrado", "disgustado", "arrogante", "molesto"], 
		["deseoso", "nervioso", "bromista", "convencido"]]
	}
</script>

<svelte:head>
	<link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
</svelte:head>


{#if page == "game"}
<button 
	on:click="{() => {pressed = true; page="home";}}"
	on:keypress="{() => {pressed = true; page = "home";}}"
	on:mouseenter="{() => pressed = false}"
>Exit</button>
{:else}
<W3Menu bind:page={page} />
{/if}

{#if page == "config"} <Config bind:params bind:log></Config>
{:else if page == "game"} <Game bind:params bind:log></Game>
{:else if page == "info"} <Info></Info>
{:else if page == "story"} <Story bind:params bind:page></Story>
{:else if page == "test"} <Test bind:params bind:page></Test>
{:else} <Home bind:params bind:page></Home>
{/if}

<style>
	:global(body){
		 margin:0px;
	 	 padding:0px;
	}
</style>
