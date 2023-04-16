<script>
  let player = null

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

<button on:click={goFullscreen}>
  <video loop bind:this={player} src="/video.mp4" class="h-screen w-screen">
    <track kind="captions" />
  </video>
</button>
