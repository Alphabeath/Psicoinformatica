<script>
    import Eyes from "./eyes.svelte";
    export let params;
    let numbers = [1, 2, 3];
    numbers = numbers.sort(() => Math.random() - 0.5);
    let index = 0;
    let count = 0;
    let n = numbers[index];
    let showFirstGroup = true;
    let finished = false;
    export let page = "test";
    function switchGroup() {
      showFirstGroup = !showFirstGroup;
    }
    function reset() {
        if(count >= numbers.length-1) {
            finished = true;
        }else{
            count++;
            index = (index + 1) % numbers.length;
            n = numbers[index];
            showFirstGroup = true;
        }
    }
  </script>
  
  <div class="container">
    <div class="column">
      <div class="row">
        <div class="cont-img">
          <Eyes {n}></Eyes>
        </div>
      </div>
      {#if showFirstGroup}
        <div class="row">
            <p style="text-align: center">¿Qué emoción/sentimiento tiene?</p>
          <div class="buttons">
            <button on:click={switchGroup}>{params.AnswerEyes[n-1][0]}</button>
            <button on:click={switchGroup}>{params.AnswerEyes[n-1][1]}</button>
            <button on:click={switchGroup}>{params.AnswerEyes[n-1][2]}</button>
            <button on:click={switchGroup}>{params.AnswerEyes[n-1][3]}</button>
          </div>
        </div>
      {:else}
        <div class="row">
          <p style="text-align: center;"> En la escala de 1 - 7 qué tan intensa es la emoción/sentimiento escogida</p>
          <p style="text-align: center;"> Donde 1 es muy baja y 7 es muy alta</p>
          <div class="buttons">
            <button on:click={reset}>1</button>
            <button on:click={reset}>2</button>
            <button on:click={reset}>3</button>
            <button on:click={reset}>4</button>
            <button on:click={reset}>5</button>
            <button on:click={reset}>6</button>
            <button on:click={reset}>7</button>
          </div>
        </div>
      {/if}
      {#if finished}
      <div class="center-button">
        <button on:click={()=>{page="home"}}> Finalizar test</button>
      </div>
      {/if}
    </div>
  </div>
<style>
    .center-button {
    margin-top: 2rem;
    display: flex;
    justify-content: center;
  }
  .center-button button{
    background-color: red;
    color: white;
    border-radius: 0.5em;
  }
  .cont-img {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .container {
    display: flex;
  }
  .column {
    flex: 1;
    padding: 1em;
  }
  .buttons {
    display: flex;
    justify-content: center;
  }
  button {
    margin: 0 1em;
  }
</style>
