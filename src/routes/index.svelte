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
  <div class="w-screen h-available fixed inset-0 z-40 border-secondary text-secondary border-[8px] md:border-[16px] pointer-events-none flex flex-col">
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
              <span class="text-xs opacity-50">0x71C7…976F</span>
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

  </div>

  <!-- Bottom fixed content -->
  <div class="w-full fixed bottom-0 inset-x-0 z-30 bg-gradient-to-t from-primary to-transparent flex justify-between">
    <!-- Tokens -->
    <div class="pointer-events-auto text-white m-3 mb-10 md:m-7 md:mb-14 flex flex-col">
      <span class="text-sm mx-2 opacity-50">Tokens</span>
      <a href="#tokens" class="flex -space-x-2 hover:bg-white hover:bg-opacity-30 transition-colors p-2 rounded-full">
        {#each Array(4) as _, index}
          <img class="rounded-full w-8 h-8 md:w-10 md:h-10 border-2 border-primary" src="/tokens/{index+1}.png" alt="token {index+1}">
        {/each}
        <span class="flex-shrink-0 w-8 h-8 md:w-10 md:h-10 bg-secondary text-primary flex items-center justify-center rounded-full border-2 border-primary text-xs font-bold">
          <span class="opacity-50">+8</span>
        </span>
      </a>
    </div>

    <!-- Friends -->
    <div class="pointer-events-auto text-white m-3 mb-10 md:m-7 md:mb-14 flex flex-col">
      <span class="text-sm mx-2 opacity-50">Friends</span>
      <a href="#tokens" class="flex -space-x-2 hover:bg-white hover:bg-opacity-30 transition-colors p-2 rounded-full">
        {#each Array(4) as _, index}
          <img class="rounded-full w-8 h-8 md:w-10 md:h-10 border-2 border-primary" src="/friends/{index+1}.png" alt="token {index+1}">
        {/each}
        <span class="flex-shrink-0 w-8 h-8 md:w-10 md:h-10 bg-secondary text-primary flex items-center justify-center rounded-full border-2 border-primary text-xs font-bold">
          <span class="opacity-50">+4</span>
        </span>
      </a>
    </div>
  </div>

  <!-- Scrollable content -->
  <div
    class="relative z-20 w-screen h-available overflow-hidden overflow-y-auto scroll-snap"
    on:scroll={handleScroll}
  >

    <!-- User profile -->
    <section class="w-screen h-available grid place-items-center">
      <div class="text-center space-y-10 drop-shadow-2xl z-20 p-[10vw]">
        <h1 class="text-secondary text-5xl xl:text-[100px] font-bold">Vitalik Buterin</h1>
        <p class="max-w-2xl mx-auto text-xs lg:text-base">Curabitur suscipit lectus lorem, convallis convallis est blandit quis. Nunc sagittis at leo eu faucibus. Maecenas rutrum lorem eros, ut sollicitudin urna blandit vel.</p>
        <ul class="flex items-center justify-center space-x-8">
          <li><a class="w-10 h-10 bg-white bg-opacity-0 transition-colors duration-200 rounded-full flex items-center justify-center hover:bg-secondary hover:text-primary" href="#Twitter"><svg class="w-6 h-6" fill="currentColor" role="img" viewBox="0 0 24 24"><title>Twitter</title><path d="M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"/></svg></a></li>
          <li><a class="w-10 h-10 bg-white bg-opacity-0 transition-colors duration-200 rounded-full flex items-center justify-center hover:bg-secondary hover:text-primary" href="#Twitch"><svg class="w-6 h-6" fill="currentColor" role="img" viewBox="0 0 24 24"><title>Twitch</title><path d="M11.571 4.714h1.715v5.143H11.57zm4.715 0H18v5.143h-1.714zM6 0L1.714 4.286v15.428h5.143V24l4.286-4.286h3.428L22.286 12V0zm14.571 11.143l-3.428 3.428h-3.429l-3 3v-3H6.857V1.714h13.714Z"/></svg></a></li>
          <li><a class="w-10 h-10 bg-white bg-opacity-0 transition-colors duration-200 rounded-full flex items-center justify-center hover:bg-secondary hover:text-primary" href="#Discord"><svg class="w-6 h-6" fill="currentColor" role="img" viewBox="0 0 24 24"><title>Discord</title><path d="M20.317 4.3698a19.7913 19.7913 0 00-4.8851-1.5152.0741.0741 0 00-.0785.0371c-.211.3753-.4447.8648-.6083 1.2495-1.8447-.2762-3.68-.2762-5.4868 0-.1636-.3933-.4058-.8742-.6177-1.2495a.077.077 0 00-.0785-.037 19.7363 19.7363 0 00-4.8852 1.515.0699.0699 0 00-.0321.0277C.5334 9.0458-.319 13.5799.0992 18.0578a.0824.0824 0 00.0312.0561c2.0528 1.5076 4.0413 2.4228 5.9929 3.0294a.0777.0777 0 00.0842-.0276c.4616-.6304.8731-1.2952 1.226-1.9942a.076.076 0 00-.0416-.1057c-.6528-.2476-1.2743-.5495-1.8722-.8923a.077.077 0 01-.0076-.1277c.1258-.0943.2517-.1923.3718-.2914a.0743.0743 0 01.0776-.0105c3.9278 1.7933 8.18 1.7933 12.0614 0a.0739.0739 0 01.0785.0095c.1202.099.246.1981.3728.2924a.077.077 0 01-.0066.1276 12.2986 12.2986 0 01-1.873.8914.0766.0766 0 00-.0407.1067c.3604.698.7719 1.3628 1.225 1.9932a.076.076 0 00.0842.0286c1.961-.6067 3.9495-1.5219 6.0023-3.0294a.077.077 0 00.0313-.0552c.5004-5.177-.8382-9.6739-3.5485-13.6604a.061.061 0 00-.0312-.0286zM8.02 15.3312c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9555-2.4189 2.157-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.9555 2.4189-2.1569 2.4189zm7.9748 0c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9554-2.4189 2.1569-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.946 2.4189-2.1568 2.4189Z"/></svg></a></li>
        </ul>
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
