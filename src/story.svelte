<script>
  export let params;
  export let page = "story";
</script>

<main>
  <div class="container">
    <h1>Historia</h1>
    {#if params.historia === 1}
      <h2>Situacion Entrevistado</h2>
      <p class="centered-paragraph">
        Me encontraba en la sala de espera, con mi currículum en mano y nervios
        revoloteando en mi estómago. El tiempo parecía detenerse mientras
        aguardaba mi turno. La puerta se abrió y fui invitado a entrar. Me
        encontré frente a un entrevistador, sentado en su imponente silla,
        mientras yo ocupaba un asiento más bajo, lo que intensificaba la
        sensación de incertidumbre. "Cuéntame un poco sobre ti", comenzó él, y
        cada palabra que salía de mi boca parecía sometida a su escrutinio. Sus
        ojos analizaban cada gesto mío, y su tono firme dejaba claro quién tenía
        el control. Me esforzaba por transmitir confianza, pero mi
        vulnerabilidad estaba a flor de piel. Al final, el apretón de manos fue
        firme, pero no pude evitar sentir la brecha de poder que separaba
        nuestras posiciones. Salí de la habitación con la incertidumbre
        carcomiéndome, consciente de que mi destino laboral estaba en manos de
        alguien que había jugado con mis emociones y mi vulnerabilidad.
      </p>
      <!-- <audio src="/Entrevistado.mp3" autoplay></audio> -->
      <div class="container">
        <h2>Realizar test</h2>
        <button
          on:click={() => {
            params.mode = "vulnerabilidad";
            page = "test";
          }}
        >
          Comenzar test
        </button>
      </div>
    {:else}
      <h2>Situacion Entrevistador</h2>
      <p>
        Como entrevistador, me encontré sentado en mi imponente silla de cuero
        en la esquina de la sala de conferencias. La mesa de roble separaba mi
        presencia de la persona que aguardaba al otro lado. Observé cada gesto,
        en el rostro del entrevistado mientras esperaba su turno. "Por favor,
        siéntese", dije con una sonrisa sutil pero amigable, aunque manteniendo
        mi tono firme. La idea era establecer la jerarquía desde el principio.
        La tensión en el aire se volvía palpable mientras él se sentaba. Durante
        la entrevista, formulé preguntas estratégicas para desentrañar sus
        experiencias pasadas y observar sus reacciones. Cada palabra pronunciada
        llevaba consigo el peso de mi evaluación. La dinámica era clara: yo
        dictaba el destino de su carrera, y él luchaba por causar una impresión
        favorable. Al final, le ofrecí una sonrisa cálida y un apretón de manos
        firme. "Nos pondremos en contacto pronto"
      </p>
      <audio src="/Entrevistador.mp3" autoplay></audio>
      <div class="container">
        <h2>Realizar test</h2>
        <button
          on:click={() => {
            params.mode = "poder";
            page = "test";
          }}
        >
          Comenzar test
        </button>
      </div>
    {/if}
  </div>

  
</main>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .container button {
    background-color: green;
    color: white;
    border-radius: 0.5em;
  }

  .container p {
    max-width: 800px; /* Ajusta este valor a lo que necesites */
    text-align: justify;
    margin: 0 auto;
  }
</style>
