<script>
  
  import Movie from './Movie.svelte';

  let searchValue = ''
  let loading = false
  let response = []

$: if (searchValue.length > 2) {
  loading = true
  fetch(`https://www.omdbapi.com/?s=${searchValue}&apikey=305e71fb`)
    .then(res => res.json())
    .then(apiResponse => {
      response = apiResponse.Search || []
      loading = false
    })
}

const handleInput = (event) => 
  searchValue = event.target.value
  
</script>

<input 
  type="text"
  on:input={handleInput}
  placeholder="Spiderman"
  value={searchValue}
>

{#if loading}
  <strong>Loading...</strong>
{:else}
  {#each response as {Title, Poster, Year}, index}
    <Movie 
      poster={Poster}
      title={Title}
      year={Year}
    />
  {:else}
    <strong>No hay resultados</strong>
  {/each}
{/if}

<style>

</style>