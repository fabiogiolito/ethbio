<script>
  import { fade, fly } from 'svelte/transition';

  export let images;

  let selectedImage = null;

  function selectImage(index) {
    selectedImage = index;
  }
</script>

<div class="container mx-auto pt-[12vh] pb-[200px]">

  <!-- Grid -->
  <div class="grid grid-cols-2 gap-4 px-[10vw] lg:grid-cols-4 lg:gap-10">
    {#each images as title, index}
      <a
        href="#link"
        class="bg-white bg-opacity-10 p-3 rounded-xl transition-all ease-in-out duration-300 hover:bg-opacity-25 hover:scale-105"
        on:click|preventDefault={(e) => selectImage(index)}
      >
        <img src="/nfts/{index + 1}.png" alt="nft {index + 1}" class="block rounded mb-2">
        <span class="block truncate text-center text-white text-xs md:text-sm xl:text-base">{title}</span>
      </a>
    {/each}
  </div>

  <!-- Selected -->
  {#if selectedImage}
    <div class="fixed w-screen h-available inset-0 grid place-items-center z-30">
      <button transition:fade={{ duration: 100 }} class="absolute inset-0 w-full h-full bg-black bg-opacity-50 backdrop-blur transition-all" on:click={() => selectImage(null)} />
      <img transition:fly={{ y: 40, duration: 250 }} class="relative z-10 drop-shadow-2xl" src="/nfts/{selectedImage + 1}.png" alt="nft {selectedImage + 1}">
    </div>
  {/if}

</div>
