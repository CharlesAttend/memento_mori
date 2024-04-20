<script>
  export let id;
  export let isPast;
  export let isEvent
</script>

<div
  {id}
  class="justify-self-stretch self-stretch place-self-stretch rounded bg-white w-full aspect-square p-[15%]"
>
  <div
    class="w-full aspect-square"
    class:bg-gray-400={isPast}
    class:bg-red-500={isEvent}
  ></div>
</div>
