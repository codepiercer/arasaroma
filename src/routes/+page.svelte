<script>
  import { onMount } from 'svelte'
  import { slide } from 'svelte/transition'

  const TOTAL_IMAGES = 20
  const IMAGES = new Array(TOTAL_IMAGES).fill(0).map((_, i) => i)
  let activeImage = 1

  // loop through images every 5 seconds and update activeImage
  onMount(() => {
    const internal = setInterval(() => {
      activeImage = (activeImage + 1) % TOTAL_IMAGES
    }, 6000)
    return () => clearInterval(internal)
  })

  // on double click, toggle between fullscreen and not
  const goFullscreen = () => {
    const el = document.documentElement
    const rfs =
      el.requestFullscreen ||
      el.webkitRequestFullScreen ||
      el.mozRequestFullScreen ||
      el.msRequestFullscreen
    const d = document
    const cfs =
      d.exitFullscreen || d.webkitExitFullscreen || d.mozCancelFullScreen || d.msExitFullscreen
    if (!d.fullscreenElement) {
      rfs.call(el)
    } else {
      cfs.call(d)
    }
  }
</script>

<button on:click={goFullscreen}>
  {#each IMAGES as i}
    {#if i === activeImage}
      <img
        transition:slide={{ delay: 1000, duration: 1000 }}
        src="/images/{activeImage}-min.jpg"
        class="h-screen w-screen object-cover"
        alt=""
      />
    {/if}
  {/each}
</button>
