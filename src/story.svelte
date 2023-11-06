<script>
    export let params;
    export let page = "story";
</script>

<main>
    <div class="container">
        <h1>Historia </h1>
        {#if params.historia === 1}
    <h2>Situacion Trabajador</h2>
        <p>Imagina que eres un empleado dedicado en tu primera semana en un nuevo trabajo. <br>
            Te sientes vulnerable y ansioso mientras esperas tu primera reunion con tu nuevo supervisor. <br>
            Te citaron a su oficina y, al entrar, te encuentras frente a su escritorio, con una silla de espaldas a la puerta. <br>
            Los nervios te invaden mientras te sientas, temiendo lo que el supervisor pueda decir sobre tu desempeno en tu primer trabajo en la empresa. <br> 
            Las palabras del supervisor, aunque bien intencionadas, hacen que te sientas aun mas vulnerable y ansioso. <br>
            Te esfuerzas por mantener la compostura y asimilar sus comentarios con dignidad. <br>
        </p>
    {:else}
    <h2>Situacion Supervisor</h2>
    <p>Imagina que eres un nuevo supervisor, te sientes completamente seguro y empoderado durante la reunion con tu nuevo empleado. <br>
        Has preparado cuidadosamente la evaluacion de su desempeno y estas listo para guiar la conversacion. <br>
        Te sientas detras de su escritorio con la espalda erguida y una expresion de seguridad en tu rostro. <br>
        Sabes que tiene el control de la situacion. Cada comentario que haces al trabajador esta respaldado por datos concretos, y manejas la reunion con autoridad. <br> 
        Reflejas confianza en su lenguaje corporal y su capacidad para brindar criticas constructivas de manera firme pero respetuosa, demostrando que esta en una posicion de poder.
    </p>
    
    {/if}
    </div>
    
    
    
    <div class="container">
        <h2>Realizar test</h2>
    <button on:click={()=>{params.mode="eye"; page="test"}}> Comenzar test </button>
    </div>
    
    

</main>

<style>
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .container button{
        background-color: green;
        color: white;
        border-radius: 0.5em;
    }
</style>