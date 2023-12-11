<script>
    export let params;
    export let log;
    export let page = "finish";

    function fileName() {
		return dateInOrgmodeFormat()+ " " + params.learner + " trained by " + params.teacher;
	}
</script>

<style>
    .mensaje {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        font-size: 2em;
        text-align: center;
        padding: 0 1em;
    }

    @media (max-width: 600px) {
        .mensaje {
            font-size: 1.5em;
        }
    }
</style>

<div class="mensaje">
    <p>¡Gracias por realizar el test!</p>

    <button><a download="{fileName()}.csv" href="{URL.createObjectURL(log.csv)}" id="downloadLinkCSV">Descargar respuestas del test</a></button>

</div>