<script>
  import Box from "$lib/components/Box.svelte";
  const updateGrid = () => {
    let tmp = [];
    for (let i = 0; i < maxAge; i++) {
      for (let j = 0; j < weeks; j++) {
        tmp.push({ id: [j, i], colored: i < age });
      }
    }
    // Update the grid (to trigger a re-render)
    grid = tmp;
  };

  $: innerWidth = 0;
  $: innerHeight = 0;
  let age = 22;

  let weeks = 52;
  let maxAge = 100;
  let grid = [];
  updateGrid();
</script>

<svelte:window bind:innerWidth bind:innerHeight />

<h1 class="text-3xl font-bold underline">Your life</h1>
<div>
  <input
    type="number"
    bind:value={age}
    on:change={updateGrid}
    class="border border-gray-300 rounded-md p-2"
  />
</div>
<div class="h-min w-full p-5">
  <div
    class="grid gap-[4px] h-full"
    style=" grid-template-rows: repeat({maxAge}, 1fr); 
            grid-template-columns: repeat({weeks / 2}, 1fr);"
  >
    {#each grid as box}
      <Box {...box} />
    {/each}
  </div>
</div>

<style lang="postcss">
  :global(html) {
    background-color: theme(colors.gray.200);
  }
</style>
