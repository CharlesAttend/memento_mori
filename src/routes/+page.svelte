<script>
  import Box from "$lib/components/Box.svelte";
  const generateGrid = () => {
    let tmp = [];
    for (let i = 0; i < maxAge; i++) {
      // age
      for (let j = 0; j < weeks; j++) {
        // weeks
        tmp.push({
          id: [j, i],
          isPast: i < currentAge,
          isEvent: j % eventFreq == 0,
        });
      }
    }
    // Update the grid (to trigger a re-render)
    return tmp;
  };

  const updateGrid = () => {
    let isPast;
    let isEvent;
    for (let i = 0; i < grid.length; i++) {
      isPast = grid[i].id[1] < currentAge;
      if (grid[i].isPast != isPast) {
        grid[i].isPast = isPast;
      }

      isEvent = grid[i].id[0] % eventFreq == 0;
      if (grid[i].isEvent != isEvent) {
        grid[i].isEvent = isEvent;
      }
    }
  };

  $: innerWidth = 0;
  $: innerHeight = 0;
  let rowPerYear = 2;
  let currentAge = 22;
  let weeks = 52;
  let maxAge = 100;
  let eventFreq = 52;
  $: remainingEvents = ((maxAge - currentAge) * weeks) / eventFreq;
  $: pastEvents = (currentAge * weeks) / eventFreq;
  $: percentagePastEvents = (100 * pastEvents) / (pastEvents + remainingEvents);
  let grid = generateGrid();
</script>

<!-- <svelte:window bind:innerWidth bind:innerHeight /> -->

<h1 class="text-3xl font-bold underline">Your life</h1>
<div>
  <input
    type="number"
    bind:value={currentAge}
    on:change={updateGrid}
    class="border border-gray-300 rounded-md p-2"
  />
  <input
    type="number"
    bind:value={maxAge}
    on:change={updateGrid}
    class="border border-gray-300 rounded-md p-2"
  />
  <input
    type="number"
    bind:value={eventFreq}
    on:change={updateGrid}
    class="border border-gray-300 rounded-md p-2"
  />
  <div>Remaining Events: {remainingEvents.toPrecision(4)}</div>
  <div>Past Events: {pastEvents.toPrecision(4)}</div>
  <div>Percentage Past Events: {percentagePastEvents.toPrecision(4)}%</div>
</div>
<div class="h-min w-full p-5">
  <div
    class="grid gap-[4px] h-full"
    style=" grid-template-rows: repeat({maxAge}, 1fr); 
            grid-template-columns: repeat({weeks / rowPerYear}, 1fr);"
  >
    {#each grid as box (box.id)}
      <Box {...box} />
    {/each}
  </div>
</div>

<style lang="postcss">
  :global(html) {
    background-color: theme(colors.gray.200);
  }
</style>
