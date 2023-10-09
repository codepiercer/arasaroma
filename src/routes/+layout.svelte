<script>
  import "../app.postcss"
</script>

<slot />

<style>
  :global(html),
  :global(body) {
    width: 1920px;
    height: 1080px;
    overflow: hidden;
  }
</style>
