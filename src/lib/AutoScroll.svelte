<script>
  export let images;
  export let transition = 0;

  let duration;
  let repeat = 2;

  let block;
  $: if (block) setDuration();

  function setDuration() {
    repeat = 2 + Math.ceil(block.offsetHeight / window.innerHeight);
    duration = 100 * (block.offsetHeight / window.innerHeight) + "s";
  }
</script>

<!-- Update speed on screen resize -->
<svelte:window on:resize={setDuration}></svelte:window>

<!-- Container -->
<div
  class="pointer-events-none w-screen h-available fixed z-10 inset-0 overflow-hidden"
  style="
    filter: blur({ transition * 40 }px);
    opacity: { 0.5 - (0.5 * transition)};
  "
>

  <!-- Duplicated so it loops correctly -->
  {#each Array(repeat) as _}
    <div
      bind:this={block}
      class="text-center animate-scroll transition-all"
      style="animation-duration: {duration};"
    >
      {#each images as _, index}
        <span class="inline-block w-[30vw] p-[5vw] xl:w-[40vw]">
          <img class="w-full h-full" src="/nfts/{index + 1}.png" alt="nft {index + 1}" />
        </span>
      {/each}
    </div>
  {/each}

</div>
