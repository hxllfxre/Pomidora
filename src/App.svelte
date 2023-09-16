<script lang="ts">
  let timer
  let ticking
  let minutes
  let seconds

  function time() {
  }
  setInterval(time, 1000)
</script>

<main class="w-screen h-screen flex items-center justify-center flex-col bg-black">
  <h1 class="text-white text-6xl font-extrabold">Pomidora</h1>
  <div class="flex">
    <h1 bind:this={minutes} class="text-3xl font-extrabold text-white">25:</h1>
    <h1 bind:this={seconds} class="text-3xl font-extrabold text-white">00</h1>
  </div>
  <button on:click={()=>time()} class="text-white border-white border-2 p-5 rounded-3xl mt-14">
    Start Timer
  </button>
</main>
