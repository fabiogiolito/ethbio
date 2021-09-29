<script>
  export let text = "Hello"

  let usableText;
  $: usableText = text;

  let repeat = 1;

  let container;
  $: if (container) setRepeat()

  function setRepeat() {
    let textWidth = container.firstChild.offsetWidth;
    repeat = 2 + Math.ceil(container.offsetWidth / textWidth);
  }
</script>

<svelte:window on:resize={setRepeat}></svelte:window>

<div class="opacity-25 whitespace-nowrap flex" bind:this={container}>
  {#each Array(repeat) as _}
    <span class="animate-marquee">{usableText}&nbsp;•&nbsp;</span>
  {/each}
</div>
