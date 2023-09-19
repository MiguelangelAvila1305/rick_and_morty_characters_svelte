<script>
  import Character from "./lib/Character.svelte";
  let characters = [];
  let page = 1;
  async function loadCharacters() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    characters = data.results;
    console.log(data);
  }

  function nextPage() {
    page++;
    loadCharacters();
  }

  function previousPage() {
    page--;
    loadCharacters();
  }

  loadCharacters();
</script>

<div class="bg-gray-900 p-4">
  <h1 class="text-5xl text-center font-bold text-white">
    Rick and Morty Characters 
  </h1>

  
    {#if page === 1}
    <div class="flex mt-6 mr-6 justify-end">
      <div>
        <button
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded m-4"
          on:click={nextPage}>Next</button
        >
      </div>
    </div>
    {:else}
    <div class="flex mt-6 mr-6 flex-row">
      <div class="basis-1/2">
        <button
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded m-4"
          on:click={previousPage}>Previous</button
        >
      </div>
      <div class="basis-1/2 text-end">
        <button
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded m-4"
          on:click={nextPage}>Next</button
        >
      </div>
    </div>
    {/if}
  

  <div class="grid grid-cols-4">
    {#each characters as character}
      <div class="bg-slate-700 rounded-xl p-2 max-w-xs m-3">
        <Character {character} />
      </div>
    {/each}
  </div>
</div>
