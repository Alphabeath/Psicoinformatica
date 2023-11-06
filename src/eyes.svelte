<script>
  export let n = 1;
</script>

{#if n == 3}
  <img src = "eyes/3.jpg" alt = "Imagen ojos 3"/>
{:else if n == 2}
  <img src = "eyes/2.jpg" alt = "Imagen ojos 2"/>
{:else if n == 1}  
  <img src = "eyes/1.jpg" alt = "Imagen ojos 1"/>
{/if}