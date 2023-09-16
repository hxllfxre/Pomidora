<script lang="ts">
  let timer

  function time() {
    
  }
  setInterval(time, 1000)
</script>

<main class="w-screen h-screen flex items-center justify-center flex-col bg-black">
  <h1 class="text-white text-6xl font-extrabold">Pomidora</h1>
  <h1 bind:this={timer} class="text-white text-4xl font-extrabold">25:00</h1>
  <button class="text-white border-white border-2 p-5 rounded-3xl mt-14">
    Start Timer
  </button>
</main>
