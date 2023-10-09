<script>
  import { fly } from "svelte/transition"
  import { onMount } from "svelte"

  import { images } from "$lib/data"

  let activeImageIdx = 0
  $: activeImage = images[activeImageIdx]

  onMount(() => {
    const interval = setInterval(() => {
      activeImageIdx = (activeImageIdx + 1) % images.length
    }, 8000)
    return () => clearInterval(interval)
  })
</script>

<img src="/cover.jpg" alt="Variety of food menus in background" class="absolute inset-0 -z-10 h-full w-full object-cover" />

<main class="relative grid h-full grid-cols-7 overflow-hidden bg-gray-900/80 backdrop-blur-sm">
  <div class="col-span-3 flex flex-col items-center overflow-hidden">
    <div class="flex flex-col items-center">
      <div class="flex items-center p-8 pb-12">
        <img src="/favicon.jpg" alt="Aras Aroma logo" class="ml-24 h-28 w-28 rounded-3xl" />
        <img src="/flags.png" alt="Canada and Italy country flags" class="ml-60 h-28" />
      </div>
      <h1 class="-mt-36 p-8 text-center font-[Sign] text-[9rem] font-extrabold tracking-wider text-white">Aras Aroma</h1>

      <div class="flex flex-col items-center justify-center px-2">
        <div class="mb-4 mt-8 flex gap-4 rounded-lg bg-black/50 p-6 pt-8 text-5xl text-yellow-500">
          <div>Take Out</div>
          |
          <div>Dine In</div>
          |
          <div>Delivery</div>
          |
          <div>Catering</div>
        </div>
        <p class="mt-8 rounded-lg bg-black/50 p-6 pt-12 text-8xl text-yellow-400">905-640-6505</p>
        <p class="mt-8 rounded-lg bg-black/50 p-6 pt-12 text-5xl text-yellow-400">Wed - Mon: 10:30am - 9:30pm</p>
      </div>
    </div>
    <div class="flex-1"></div>
    <img src="/delivery.png" alt="Delivery partners" class="h-48" />
  </div>
  <div class="relative col-span-4 flex h-full flex-col rounded-l-full bg-gray-900/80">
    {#key activeImageIdx}
      <img
        in:fly={{ x: 500, y: -500, duration: 2000, delay: 500 }}
        out:fly={{ x: 500, y: 500, duration: 3000 }}
        src={`/menu/` + activeImage.src}
        alt={activeImage.alt}
        class="absolute inset-0 left-6 h-full w-full rounded-full"
      />
      <img
        in:fly={{ duration: 2000, delay: 2000 }}
        out:fly={{ duration: 500 }}
        src="/smoke.gif"
        alt="Food smoke effect"
        class="absolute inset-0 h-full w-full -translate-y-96"
      />
      <div
        in:fly={{ duration: 2000, delay: 500 }}
        out:fly={{ duration: 1000 }}
        class="absolute bottom-0 right-0 h-fit w-fit rounded-lg bg-black/50 p-10 backdrop-blur-sm"
      >
        <h2 class="text-8xl text-white">{activeImage.alt}</h2>
      </div>
    {/key}
  </div>
</main>
