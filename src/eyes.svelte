<script>
  export let n = 1;
</script>

<img src={`eyes/${n}.jpg`} alt={`Imagen ojos ${n}`} />

<style>
  @media (max-width: 480px) {
    img {
    width: 100%;
  }
  }
 
</style>