<script>
  export let id;
  export let colored;
</script>

<div
  {id}
  class="justify-self-stretch self-stretch place-self-stretch rounded bg-white w-full aspect-square p-[15%]"
>
  <div
    class="w-full aspect-square"
    class:bg-gray-400={colored}
  ></div>
</div>
