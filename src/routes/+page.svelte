<script>
  import { onMount } from 'svelte'
  import { fade } from 'svelte/transition'

  const TOTAL_IMAGES = 16
  const IMAGES = new Array(TOTAL_IMAGES).fill(0).map((_, i) => i)
  let activeImage = 0
  let player = null

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
      player.play()
    } else {
      cfs.call(d)
      player.pause()
    }
  }
</script>

<audio loop bind:this={player}>
  <source src="/music.mp3" type="audio/mpeg" />
</audio>

<button on:click={goFullscreen}>
  {#each IMAGES as i}
    {#if i === activeImage}
      <img
        transition:fade={{ delay: -500, duration: 1000 }}
        src="/images/{activeImage}-min.jpg"
        class="h-screen w-screen object-fill"
        alt=""
      />
    {/if}
  {/each}
</button>
