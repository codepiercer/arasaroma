<script>
  import "../app.postcss"
</script>

<slot />

<style>
  :global(html),
  :global(body) {
    height: 1080px;
    width: 2560px;
  }
</style>
