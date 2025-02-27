<script>
  export let poster, title, year
</script>

<article>
  <img src={poster} alt={title}>
  <h3>{title}</h3>
  <span>{year}</span>
  {#if 2024 - year < 5}
    <strong>Pelicula nueva</strong>
  {/if}
</article>

<style>
  article {
    border: 1px solid #eee;
    border-radius: 4px;
    margin-bottom: 8px;
    padding: 16px;
  }

  h3 {
    font-size: 24px;
    margin-bottom: 4px;
  }
</style>