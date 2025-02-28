<script>
  // @ts-nocheck
  import Movie from './Movie.svelte';
  
  let searchValue = ''
  let response = []

  const handleInput = (event) => 
  searchValue = event.target.value
  
  $: if (searchValue.length > 2) {
  response = fetch(`https://www.omdbapi.com/?s=${searchValue}&apikey=305e71fb`)
    .then(res => !res.ok && new Error('something goes wrong'))
    .then(res => res.json())
    .then(apiResponse => apiResponse.Search || [])
}

</script>

<input 
  type="text"
  on:input={handleInput}
  placeholder="Spiderman"
  value={searchValue}
>

{#await response}
  <strong>Loading...</strong>
{:then movies}
  {#each movies as {Title, Poster, Year}, index}
    <Movie 
      poster={Poster}
      title={Title}
      year={Year}
    />
  {:else}
    <strong>No hay resultados</strong>
  {/each}
{/await}

<style>

</style>