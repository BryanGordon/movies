<script>

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
  
$: console.log(searchValue)

</script>

<input 
  type="text"
  on:input={handleInput}
  placeholder="Spiderman"
  value={searchValue}
>

{#if loading}
  <strong>Loading...</strong>
{:else if response.length > 0}
  <strong>Tenemos {response.length} peliculas</strong>
  {:else}
    <strong>No hay resultados</strong>
{/if}

<style>

</style>