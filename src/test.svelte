<script>
  import Eyes from "./eyes.svelte";
  import { dateInOrgmodeFormat } from "./log.js";
  export let params;
  export let page = "test";
  export let log = {};
  let numbers = Array.from({ length: 36 }, (_, i) => i + 1);
  log.time_last_display = Date.now();
  numbers = numbers.sort(() => Math.random() - 0.5);
  let index = 0;
  let count = 0;
  let n = numbers[index];
  let showFirstGroup = true;
  let finished = false;
  let indices = [0, 1, 2, 3];
  let selected = "";

  function fileName() {
    return (
      dateInOrgmodeFormat() +
      " " +
      params.learner +
      " trained by " +
      params.teacher
    );
  }

  function enterInCSVLog(string) {
    console.log(string);
    log.csv_diary = [...log.csv_diary, "\n" + string];
    log.csv = new Blob(log.csv_diary, { type: "text/csv" });
  }
  function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
    return array;
  }

  function switchGroup(string) {
    showFirstGroup = !showFirstGroup;
    selected = string;
    console.log("Selected es " + selected);
  }
  function reset(string) {
    log.test_number++;
    if (count > numbers.length - 1) {
      finished = true;
    } else {
      var response_time = Date.now() - log.time_last_display;
      let correctitud = "Incorrecto";
      if (selected == params.AnswerEyes[n - 1][0]) {
        correctitud = "Correcto";
      }
      let intesity = string;
      enterInCSVLog(
        log.test_number +
          ", " +
          params.mode +
          ", " +
          params.learner +
          ", " +
          params.teacher +
          ", " +
          n +
          ", " +
          selected +
          ", " +
          correctitud +
          ", " +
          intesity +
          ", " +
          params.AnswerEyes[n - 1][0] +
          ", " +
          params.AnswerEyes[n - 1][1] +
          ", " +
          params.AnswerEyes[n - 1][2] +
          ", " +
          params.AnswerEyes[n - 1][3] +
          ", " +
          dateInOrgmodeFormat() +
          ", " +
          response_time
      );
      count++;
      index = (index + 1) % numbers.length;
      n = numbers[index];
      showFirstGroup = true;
      indices = shuffleArray(indices);

      selected = "";
      log.time_last_display = Date.now();
    }
  }
</script>

<div class="container">
  <div class="column">
    {#if !finished}
    <div class="row">
      {#if params.mode == "vulnerabilidad"}
        <h3 style="text-align: center">
          Al terminar la entrevista, miras al entrevistador a los ojos
        </h3>
      {:else}
        <h3 style="text-align: center">
          Al terminar la entrevista, miras al entrevistado a los ojos
        </h3>
      {/if}
      <div class="cont-img">
        <Eyes {n} />
      </div>
    </div>
    {#if showFirstGroup}
      <div class="row">
        <p style="text-align: center">¿Qué emoción/sentimiento tiene?</p>
        <div class="buttons">
          <button
            on:click={() => switchGroup(params.AnswerEyes[n - 1][indices[0]])}
            >{params.AnswerEyes[n - 1][indices[0]]}</button
          >
          <button
            on:click={() => switchGroup(params.AnswerEyes[n - 1][indices[1]])}
            >{params.AnswerEyes[n - 1][indices[1]]}</button
          >
          <button
            on:click={() => switchGroup(params.AnswerEyes[n - 1][indices[2]])}
            >{params.AnswerEyes[n - 1][indices[2]]}</button
          >
          <button
            on:click={() => switchGroup(params.AnswerEyes[n - 1][indices[3]])}
            >{params.AnswerEyes[n - 1][indices[3]]}</button
          >
        </div>
      </div>
    {:else}
      <div class="row">
        <p style="text-align: center;">
          En la escala de 1 - 7 qué tan intensa es la emoción/sentimiento
          escogida
        </p>
        <p style="text-align: center;">Donde 1 es muy baja y 7 es muy alta</p>
        <div class="buttons">
          <button
            on:click={(e) => {
              e.stopPropagation();
              reset("1");
            }}>1</button
          >
          <button
            on:click={(e) => {
              e.stopPropagation();
              reset("2");
            }}>2</button
          >
          <button
            on:click={(e) => {
              e.stopPropagation();
              reset("3");
            }}>3</button
          >
          <button
            on:click={(e) => {
              e.stopPropagation();
              reset("4");
            }}>4</button
          >
          <button
            on:click={(e) => {
              e.stopPropagation();
              reset("5");
            }}>5</button
          >
          <button
            on:click={(e) => {
              e.stopPropagation();
              reset("6");
            }}>6</button
          >
          <button
            on:click={(e) => {
              e.stopPropagation();
              reset("7");
            }}>7</button
          >
        </div>
      </div>
    {/if}
    {/if}
    {#if finished}
  <div class="container">
    <button><a download="{fileName()}.csv" href="{URL.createObjectURL(log.csv)}" id="downloadLinkCSV">Descargar respuestas del test</a></button>
  </div>
{/if}
  </div>
</div>

<style>
  .container {
    display: flex;
    justify-content: center;
    flex-wrap: wrap; /* Añade esta línea para permitir que los elementos se envuelvan en nuevas líneas si no caben en la línea actual */
  }
  .column {
    flex: 1 0 100%; /* Cambia esto para permitir que las columnas se reduzcan a su contenido en lugar de mantener una flexión de 1 */
    padding: 1em;
    box-sizing: border-box; /* Añade esto para incluir el padding y el borde en el ancho total del elemento */
  }
  .buttons {
    display: flex;
    justify-content: center;
    flex-wrap: wrap; /* Añade esto para permitir que los botones se envuelvan en nuevas líneas si no caben en la línea actual */
  }
  button {
    margin: 0.5rem 0.5rem;
    max-width: 110px;
    flex: 1 0 auto; /* Cambia esto para permitir que los botones se reduzcan a su contenido en lugar de mantener una flexión de 1 */
  }
  @media (max-width: 768px) {
    .cont-img {
      flex-direction: column;
    }
  }
  @media (max-width: 480px) {
    .cont-img {
      flex-direction: column-reverse;
      display: flex;
    }
  }

  .cont-img {
    width: 100%;
    max-height: 25%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>
