<script>
  import AutoScroll from '$lib/AutoScroll.svelte';
  import Gallery from '$lib/Gallery.svelte';
  import QRCode from '$lib/QRCode.svelte';
  import Marquee from "$lib/Marquee.svelte";

  let nfts = [
    "Eva 01 mod",
    "Burn out",
    "Genesis 0x1",
    "The Ritual",
    "Lost Glitch #8828",
    "The Quest for the Diamond Fleece",
    "Ashes to Ashes",
    "Colonist #7532"
  ];

  let themes = [
    ["#120027", "#7505EC"],
    ["#1F2DDE", "#71FAC0"],
    ["#081B1C", "#B6D85C"],
    ["#130C0C", "#E0352E"]
  ]

  let theme;
  $: if (themes) theme = themes[Math.floor(Math.random() * themes.length)]

  let scrollY = 0;
  let scrollPercent = 0;
  let isScrolled = false;

  function handleScroll(e) {
    scrollY = e.target.scrollTop;
    scrollPercent = Math.min(scrollY / window.innerHeight, 1);
    isScrolled = scrollPercent > 0.5;
  }
</script>

<svelte:head>
  {#if theme}
    <meta name="theme-color" content="{theme[1]}">
  {/if}
</svelte:head>

<div class="font-mono bg-primary text-white"
  style="
    --color-primary: {theme[0]};
    --color-secondary: {theme[1]};
  "
>

  <!-- Fixed content (borders) -->
  <div class="w-screen h-available fixed inset-0 z-30 border-secondary text-secondary border-[16px] pointer-events-none flex flex-col">
    <div class="flex justify-between">
      <!-- Corner Top Left -->
      <svg class="flex-shrink-0 w-4 h-4 lg:w-8 lg:h-8" width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M40 0H0V40C0 17.9086 17.9086 0 40 0Z" fill="currentColor"/>
      </svg>
      <!-- Center HUD -->
      <div class="-mt-3 relative">
        <svg width="300" height="64" viewBox="0 0 300 64" fill="none">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M10.7562 12H0V0H30H270H300V12H289.244C255.984 12 259.821 64 226.671 64H73.329C40.1793 64 44.0156 12 10.7562 12Z" fill="currentColor"/>
        </svg>
        <div class="absolute w-full h-full py-3 px-16 inset-0">
          <div class="w-full h-full flex items-center justify-center space-x-3 text-primary">
            <img src="/avatar.png" class="block rounded-full w-10 h-10 ring ring-white ring-opacity-25" alt="avatar">
            <div class="flex flex-col">
              <span>@V_B</span>
              <span class="text-xs opacity-50">0xa574…c87ffa1</span>
            </div>
          </div>
        </div>
      </div>
      <!-- Corner Top Right -->
      <svg class="flex-shrink-0 w-4 h-4 lg:w-8 lg:h-8" width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M0 0H40V40C40 17.9086 22.0914 0 0 0Z" fill="currentColor"/>
      </svg>
    </div>

    <div class="flex-1" />

    <div class="flex justify-between">
      <!-- Corner Bottom Left -->
      <svg class="flex-shrink-0 w-4 h-4 lg:w-8 lg:h-8" width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M40 40H0V0C0 22.0914 17.9086 40 40 40Z" fill="currentColor"/>
      </svg>
      <!-- Corner Bottom Right -->
      <svg class="flex-shrink-0 w-4 h-4 lg:w-8 lg:h-8" width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M0 40H40V0C40 22.0914 22.0914 40 0 40Z" fill="currentColor"/>
      </svg>
    </div>

    <div class="bg-secondary text-primary pt-3 leading-none">
      <Marquee text="0x71C7656EC7ab88b098defB751B7401B5f6d8976F" />
    </div>

    <!-- Logo -->
    <div class="hidden lg:block fixed top-0 left-0 m-10"><img src="/logo.png" alt="eth.bio" /></div>

    <!-- QR Code -->
    <div class="hidden lg:block text-white fixed top-0 right-0 m-10"><QRCode /></div>

    <!-- Tokens -->
    <div class="pointer-events-auto text-white fixed bottom-0 left-0 m-7 mb-14 flex flex-col">
      <span class="text-sm mx-2 opacity-50">Tokens</span>
      <a href="#tokens" class="flex -space-x-2 hover:bg-white hover:bg-opacity-30 transition-colors p-2 rounded-full">
        {#each Array(4) as _, index}
          <img class="rounded-full w-10 h-10 border-2 border-primary" src="/tokens/{index+1}.png" alt="token {index+1}">
        {/each}
      </a>
    </div>

    <!-- Tokens -->
    <div class="pointer-events-auto text-white fixed bottom-0 right-0 m-7 mb-14 flex flex-col">
      <span class="text-sm mx-2 opacity-50">Friends</span>
      <a href="#tokens" class="flex -space-x-2 hover:bg-white hover:bg-opacity-30 transition-colors p-2 rounded-full">
        {#each Array(4) as _, index}
          <img class="rounded-full w-10 h-10 border-2 border-primary" src="/friends/{index+1}.png" alt="token {index+1}">
        {/each}
      </a>
    </div>
  </div>

  <!-- Scrollable content -->
  <div
    class="relative z-20 w-screen h-available overflow-hidden overflow-y-auto scroll-snap"
    on:scroll={handleScroll}
  >

    <!-- User profile -->
    <section class="w-screen h-available grid place-items-center p-10">
      <div class="text-center space-y-10 drop-shadow-2xl z-20">
        <img src="avatar.png" alt="avatar" class="inline-block w-40 h-40 rounded-full bg-white">
        <h1 class="text-secondary text-5xl xl:text-[100px] font-bold">Vitalik Buterin</h1>
      </div>
    </section>
    
    <!-- NFT gallery -->
    <section class="relative w-screen min-h-available z-20 overflow-hidden grid place-items-center">
      <Gallery images={nfts} />
    </section>
  </div>

  <!-- Auto scrolling images -->
  <AutoScroll images={nfts} transition={scrollPercent} />

</div>
