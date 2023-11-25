<script>
  import Quantity from "./quantity.svelte";
	import {dateInOrgmodeFormat} from "./log.js";
// Parameters of the app:
export let params ={};
export let log ={};
// Variables of the app
let potentialChoices = [1,2,3,4,5,6];
let correctSound = new Audio(params.correctSoundURL);
let incorrectSound = new Audio(params.incorrectSoundURL);
let noMoreSound = new Audio(params.noMoreSoundURL);
let excellentSound = new Audio(params.gameSoundsURLs.excel);
let passSound = new Audio(params.gameSoundsURLs.pass);
let failSound = new Audio(params.gameSoundsURLs.fail);
let choices = [];
let selection;
let selected = false;
let correct = false;
let exerciseResult = "";
let gameResult = "";
let waitingForReward=false;
let nbCorrect = 0;
let nbIncorrect = 0;	
// Initializing
reset();
newOne();
// Functions
function enterInLocalLog(string) {
 //	  console.log(dateInOrgmodeFormat()+" "+string);
  	log.text_diary = [...log.text_diary,"\n"+dateInOrgmodeFormat()+" "+string];
   	log.text = new Blob(log.text_diary, {type: 'text/plain'});
}
function enterInCSVLog(string) {
	  console.log(string);
   	log.csv_diary = [...log.csv_diary,"\n"+string];
   	log.csv = new Blob(log.csv_diary, {type: 'text/csv'});
}
function select(c){
	log.test_number ++;
	if(selected == false) {
		selected = true;
		selection = c;
		correct = true;
		var i;
		for(i=0;i<choices.length;i++){
	    if(choices[i]>selection) {
	       correct = false
			}
		}	
    var	d = new Date();
  	var response_time = Date.now()-log.time_last_display;
		var choices_complementary = ""
		if (params.nbChoices == 1) {
  		var choices_complementary = ",,,,"
			} else if (params.nbChoices == 2) {
  		var choices_complementary = ",,,"
			} else if (params.nbChoices == 3) {
  		var choices_complementary = ",,"
			} else if (params.nbChoices == 4) {
  		var choices_complementary = ","
			} else if (params.nbChoices == 5) {
  		var choices_complementary = ""
			}
   //	csv_diary: ["Test no, Test Name, Learner, Trainer, C_0, C_1, C_2, C_3, C_4, Clicked , Correction , Date, Answering Time, Other Parameters"],
		enterInCSVLog(log.test_number+", "+params.mode+", "+params.learner+", "+params.teacher+", "+choices+choices_complementary+", "+c+","+correct+", "+dateInOrgmodeFormat()+", "+response_time+", background "+params.bg+", foreground "+params.fg+", bg opacity "+params.bg_opacity+", Value Set ["+params.values.sort()+"]");
		if(correct == true) {
				nbCorrect++;
		    if(params.visualFeedback){exerciseResult=params.visualFeedbackCorrect}
				if(params.playSound){					if(nbCorrect+nbIncorrect < params.gameLength){correctSound.play();}};
				enterInLocalLog(params.learner+" chose correctly "+c+" out of "+choices+" in mode '"+params.mode+"' with "+params.fg+" stuff on "+params.bg+" background.");
		} else {
				nbIncorrect++;
	      if(params.visualFeedback){exerciseResult=params.visualFeedbackInCorrect}
				if(params.playSound){
					if(nbCorrect+nbIncorrect < params.gameLength){incorrectSound.play();}}
				enterInLocalLog(params.learner+" chose INcorrectly "+c+" out of "+choices+" in mode '"+params.mode+"' with "+params.fg+" stuff on "+params.bg+" background.");
		}
		if(params.gameFeatures){
  		if(nbCorrect+nbIncorrect >= params.gameLength) {
				enterInLocalLog(params.learner+" finished a game: "+nbCorrect+" correct answers and "+nbIncorrect+" incorrect answers.");
	  	  if(nbCorrect >= params.gameThresholds.excel*params.gameLength) {
		  		if(params.playSound){setTimeout(excellentSound.play(),params.gameWaitingTimeForResultInMiliseconds);};
	        if(params.visualFeedback){gameResult=params.visualFeedbackExcellent}
					console.log("Excellent")
			  } else if (nbCorrect>=params.gameThresholds.pass*params.gameLength) {
				  if(params.playSound){setTimeout(passSound.play(),params.gameWaitingTimeForResultInMiliseconds);};
	        if(params.visualFeedback){gameResult=params.visualFeedbackPass}
					console.log("Pass")
			  } else {
				  if(params.playSound){setTimeout(failSound.play(),params.gameWaitingTimeForResultInMiliseconds);};
	        if(params.visualFeedback){gameResult=params.visualFeedbackFail}
					console.log("Fail")
			  }	
				waitingForReward = true;
  		}
		}
		if(!waitingForReward){
  		setTimeout(() => {newOne();}, params.waiting_time*1000);
		}
	}
	}
	function reset(){
	 nbCorrect = 0;
	 nbIncorrect = 0;
	 gameResult = "";
	}	
	function newOne() {
		// Generates a random pair of distinct integers from [1..{maxNumber}]
		var i,r
		for(i=0; i<params.nbChoices; i++){
			r = Math.floor(Math.random()*(params.values.length-i));
			[params.values[i],params.values[i+r]]=[params.values[i+r],params.values[i]] // swap the two values
		}
		choices = []
		for(i=0; i<params.nbChoices; i++){
			choices = [...choices,params.values[i]]
		}
		selected = false;
		correct = false;
		exerciseResult = ""; 
  	log.time_last_display = Date.now();
	}
</script>

<h1 align="center">What's the emotion?</h1>

{#if !selected}
<div style="--nbChoices: {params.nbChoices}">
			{#each choices as c}
   	<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
		<span 
				aria-keyshortcuts="A"
				on:click={()=>select(c)}
				on:keydown={()=>select(c)}
				role="navigation">
				<Quantity n={c} 
						mode={params.mode}
						fg={params.fg}
						bg={params.bg}												  
						bg_opacity={params.bg_opacity}
						></Quantity>
		</span>
		{/each}
</div>
{:else}
{#if params.visualFeedback}
<center>{@html exerciseResult}</center>
<center>{@html gameResult}</center>
{/if}
{/if}
{#if params.noMoreBotton}
<button on:click="{() => {noMoreSound.play();}}">No more</button>
{/if}
{#if waitingForReward}
<center>
<button on:click="{() => {waitingForReward=false;reset();newOne()}}" class="for_birds">Play again?</button>
</center>
{/if}

<center>(+{nbCorrect},-{nbIncorrect}) {#if params.gameFeatures} among {params.gameLength}{/if}</center>

<style>
	span{
	margin-left: calc( (90vw - var(--nbChoices) * 160px ) / ( var(--nbChoices) + 1 ) );
	}

.for_birds {
  display: inline-block;
  width: 100px; 
  height: 100px; 
  text-align: center;
  border: gray;
  background-color: #E8562A;
  color: #fff;
  cursor: pointer;
  font-weight: bold;
}
	/*
	table{width:100%}
	td {
  text-align: center;
		border:1px solid black;
	}
	*/
	/* peut etre a creuser :
	https://developer.mozilla.org/fr/docs/Web/CSS/justify-content
	mais si on souhaiter calculer les espaces il faudrait imp�rativement connaitre la "largeur" de quantity 
	*/
	
	/*
	td {
    padding-left: 100px;
    padding-right: 0px;
  }
  td:first-child {
    padding-left: 0;
  }
  td:last-child {
    padding-right: 0;
  }*/
</style>