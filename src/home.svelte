<script>
  export let page = "home";
  export let params = {};
  let nombre = "";
  let isOpen = true;

  function openModal() {
    isOpen = true;
  }

  function closeModal() {
    isOpen = false;
  }

  function accept() {
    // Código para manejar la aceptación

    params.learner = nombre;
    closeModal();
  }

  function decline() {
    // Código para manejar el rechazo
    closeModal();
  }
</script>

<h1 align="center">Empathy and Power Relationship</h1>

{#if isOpen}
<div class="modal">
  <div class="modal-content">
    <h2>Antes de comenzar</h2>
    <span class="close-button" on:click={closeModal}>X</span>
    <a href="https://forms.office.com/r/1eWb4Wd54t"><button class="button form" on:click={decline}>Realizar Consentimiento</button></a>
    <p>Usted al presionar en "Acepto" confirma que ha realizado el cuestionario de <a href="https://forms.office.com/r/1eWb4Wd54t">Consentimiento informado</a> y está de acuerdo con los términos establecidos</p>
    <input type="text" placeholder="Ingresa tu nombre" bind:value={nombre} />
    <button class="button" on:click={accept}>Acepto</button>
    

  </div>
  </div>
{/if}
<table align="center">
  <tr>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <td width="50%"
      on:click={() => {
        params.historia = 2;
        page = "story";
      }}
    >
      <h3>Situación de poder</h3>
	  <svg fill="#e9e335" height="129px" width="129px" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 220 220" xml:space="preserve"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M220,98.865c0-12.728-10.355-23.083-23.083-23.083s-23.083,10.355-23.083,23.083c0,5.79,2.148,11.084,5.681,15.14 l-23.862,21.89L125.22,73.002l17.787-20.892l-32.882-38.623L77.244,52.111l16.995,19.962l-30.216,63.464l-23.527-21.544 c3.528-4.055,5.671-9.344,5.671-15.128c0-12.728-10.355-23.083-23.083-23.083C10.355,75.782,0,86.137,0,98.865 c0,11.794,8.895,21.545,20.328,22.913l7.073,84.735H192.6l7.073-84.735C211.105,120.41,220,110.659,220,98.865z"></path> </g></svg>
    </td>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <td
	width="50%"
      on:click={() => {
        params.historia = 1;

        page = "story";
      }}
    >
      <h3>Situación de vulnerabilidad</h3>
	  <svg width="117px" height="117px" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="m5.73 47.64a11.38 11.38 0 0 1 5.56-2.72c1.31-.09 3.28 0 4.66-.87s2.4-2.78 4.84-3 3.63-.22 4.69-.38a9.47 9.47 0 0 0 1.94-.5s-.42-6.87-1.42-13.28-2.8-12.53-2.71-12.75 1.88-.94 2-.66a3.11 3.11 0 0 1 .25.72l14.31-5.09c5.35-1.91 8.15-2.56 8.91-2.56s1.13.87.84 2.31-1 2.47.32 3.72 2.68 1.75 2.5 4.09-1.78 2.44-1 4.1 2.68 2.23 2.58 4.37-1 2.44-4.22 3.41-10.78 2.93-11.78 2.93a7.74 7.74 0 0 0 -3.41.63 43.86 43.86 0 0 0 -5.75 2c0 .19.44 5.12.44 5.12s4-1.31 5.75-.81 1.22 1.88 3.78 1.66 4.66-1.31 7.6-.38 3 2.44 5.46 3.16a11.07 11.07 0 0 1 7 5.37c1.56 3.13 1.43 7.54 1.06 8.25s-3 1-3.63 1-17.34-.9-24.15-.62-21.82.44-23.85.4a3.87 3.87 0 0 1 -4-2.43c-.79-1.78-.82-5.25 1.43-7.19z" fill="#1d1d1b"></path> <path d="m25.89 15.92c.21-.09 10.18-3.81 13.78-5s7.65-2.12 7.65-2.12-.37 2.87.53 3.9 2.88 1.91 2.5 3.72-1.62 3.19-.71 4.66 2.43 2.47 2.31 3.62-1.75 1.6-2.44 2-11.44 3.22-13.94 3.66a65.47 65.47 0 0 0 -6.9 1.91z" fill="#cbe7f5"></path> <path d="m27.89 16.92c.15 0 .75-.34.81-.12a15.58 15.58 0 0 1 .53 3.2c-.16.28-.66.5-.75.34a18.94 18.94 0 0 1 -.59-3.42z" fill="#1d1d1b"></path> <path d="m46.64 14.27c.08-.17 1.46.18 1.46.4s0 .56-.12.56a6.27 6.27 0 0 1 -1.53-.23c-.1-.14.15-.67.19-.73z" fill="#1d1d1b"></path> <path d="m46.23 17.11a9.17 9.17 0 0 1 2.5.5c0 .16-.06.69-.19.69s-2.5-.44-2.5-.44-.04-.66.19-.75z" fill="#1d1d1b"></path> <path d="m45.67 18.92a8.68 8.68 0 0 1 2.78.47c.09.25.19.69 0 .78a18.28 18.28 0 0 1 -3-.56c-.06-.06.06-.61.22-.69z" fill="#1d1d1b"></path> <path d="m45.23 21.27a9.63 9.63 0 0 1 3 .78c0 .22.09.47-.06.53a21.12 21.12 0 0 1 -3.17-.66c-.15-.09.1-.56.23-.65z" fill="#1d1d1b"></path> <path d="m44.29 23.14a29 29 0 0 1 4 1.41c0 .15-.15.65-.25.65s-4.15-1.28-4.15-1.37.28-.66.4-.69z" fill="#1d1d1b"></path> <path d="m43.17 25a17.54 17.54 0 0 1 3.83 1.36c-.06.19-.09.53-.25.56s-3.75-1.15-3.9-1.22.22-.7.32-.7z" fill="#1d1d1b"></path> <path d="m8.42 48c1.49-.7 3.37-1.72 4.81-1.78s2.47.13 4-1 2.44-2.43 4.66-2.78 4.09-.5 4.68-.59 1-.19 1-.19-.06.81.16.91a3.1 3.1 0 0 0 1.65-.16c.32-.22.25-1.53.25-1.53a6.46 6.46 0 0 1 4-.94c1.85.41 2.75 1.81 4.91 1.69s4.75-1.25 7.25-.31 1.81 2.04 3.78 2.68 5.16.75 6.88 3.88 1.81 7.15 1.47 7.44-6.28.25-12.72.06-14.38-.06-22 .15-14.6.47-15 .35a2 2 0 0 1 -1.91-1.41c-.56-1.42-1.12-4.99 2.13-6.47z" fill="#e6e4da"></path> <path d="m21.07 43.77c1.59-.26 2.19 1 1.53 2.12a1.93 1.93 0 0 1 -3 .31c-.6-.84.13-2.2 1.47-2.43z" fill="#1d1d1b"></path> <path d="m21.1 44.5c.8-.13 1.11.52.78 1.08a1 1 0 0 1 -1.53.16c-.35-.43.06-1.13.75-1.24z" fill="#ffffff"></path> <g fill="#1d1d1b"> <path d="m39 42.45c.72-.3 2.37-.43 2.47.19s-1.07 1.22-2.13 1-1.2-.84-.34-1.19z"></path> <path d="m50.82 46.8a4.19 4.19 0 0 1 3.1.65c.78.78-.66 1.5-1.32 1.5a3.14 3.14 0 0 1 -1.75-.84c-.34-.31-.56-1.19-.03-1.31z"></path> <path d="m19.17 51.52a3.27 3.27 0 0 1 1.83-2.69 8.58 8.58 0 0 1 5.31-1.22c2.59.12 2.59.69 2.41 1s-.63 1-.88 1-2.84-.84-4.84.12-2.13 1.47-2.31 1.85-1.4.19-1.52-.06z"></path> <path d="m14.67 47.89c.14 0 2.43 1.13 2.34 1.34s-.25.5-.41.5a19.66 19.66 0 0 1 -2.53-1.12c-.07-.13.47-.72.6-.72z"></path> <path d="m12.85 49.36a29.1 29.1 0 0 1 4 2.72c-.13.15-.35.5-.47.47s-4.18-2.55-4.21-2.66.53-.5.68-.53z"></path> <path d="m10.89 50.3a39.93 39.93 0 0 1 4.31 3.12.82.82 0 0 1 -.47.41 42 42 0 0 1 -4.53-3c0-.19.59-.56.69-.53z"></path> <path d="m9.07 51.39c.16 0 3.82 2.81 3.6 3s-.63.44-.75.37a33.14 33.14 0 0 1 -3.75-2.68 2.72 2.72 0 0 1 .9-.69z"></path> <path d="m26.73 44.23a11.26 11.26 0 0 1 2.91 2.13c-.07.25-.19.41-.32.37s-3.25-2.06-3.25-2.06a3.71 3.71 0 0 1 .66-.44z"></path> <path d="m28 43.67s.6-.4.81-.37a15.89 15.89 0 0 1 2.79 1.62.78.78 0 0 1 -.47.35 27.81 27.81 0 0 1 -3.13-1.6z"></path> <path d="m30.45 42.67c-.07-.08.53-.4.75-.44a18.79 18.79 0 0 1 2.4 1.5.42.42 0 0 1 -.31.22 11.68 11.68 0 0 1 -2.84-1.28z"></path> <path d="m27.35 53.48c-.17-.17 1.44-1.4 2.38-1.15s.72.72 1.28.84 1-.09 1.22 0 .34.47.22.53a2.8 2.8 0 0 1 -1.35.1c-.46-.13-1.37-.75-1.78-.63s-.78.91-1.18.82a1.71 1.71 0 0 1 -.79-.51z"></path> <path d="m52.2 50.67c.31-.06 3.56 1.85 3.47 2.13s-.13.43-.28.4-3.82-1.53-3.79-1.78.29-.69.6-.75z"></path> <path d="m50.2 52c.19 0 3.69 2.07 3.56 2.25s-.91.28-1.12.25a22.16 22.16 0 0 1 -3.22-1.84c-.03-.21.58-.66.78-.66z"></path> <path d="m35.51 45.33c1.22-.1 3.69-1.35 6-.91s5.85 1.63 5.78 4.72a4.48 4.48 0 0 1 -4.81 4.5c-2.22-.12-3.78-1.94-4.94-2.09s-4.78.53-5.53-1.91 1.22-4.12 3.5-4.31z"></path> </g> <path d="m36.17 46.77c2.07 0 4.18-1.32 6.81-.47s3.19 2.78 3.06 3.43-1.75 1.79-1.84 1.79a34.9 34.9 0 0 0 -2.91-2c-.31 0-.87.44-.72.57s2.43 1.71 2.28 1.8a2.74 2.74 0 0 1 -1.31-.12c-.59-.16-2.5-1.69-4.4-1.85s-2.91-.28-3-1.28.75-1.87 2.03-1.87z" fill="#ffffff"></path> <path d="m43.2 48.33c.23 0 2 1.09 1.94 1.28a2.24 2.24 0 0 1 -.91.66c-.13 0-1.84-1-1.78-1.19s.55-.75.75-.75z" fill="#1d1d1b"></path> </g></svg>
    </td>
  </tr>
</table>

<style>
   .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.8);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal-content {
    background-color: #fff;
    padding: 20px;
    border-radius: 4px;
    position: relative;
  background-color: #fff;
  padding: 20px;
  border-radius: 4px;
  }

  .close-button {
    position: absolute;
    right: 20px;
    top: 20px;
    cursor: pointer;
  }
  a{
    color: #4747c5;
    text-decoration: underline ;
    font-weight: 600;
  }

  .button{
    background-color: rgb(6, 156, 6);

    border-radius: 0.25rem;
    color: white;
    text-decoration: solid;
    font-weight: 400;
  }
  .button:hover{
    background-color: rgb(6, 156, 6);
    border-radius: 0.25rem;
    color: white;
  }

  .button.form{
    background-color: rgb(45, 60, 192);
    display: block;
    margin-left: auto;
    margin-right: auto;

  }
</style>



