<script lang="ts">
    import { tick } from "svelte";

  let button : any
  let ticking : Boolean = false
  let minutes : any
  let seconds : any
  let secondsV = 60
  let minutesV = 24
  let breakButton : any
  var ringtone = new Audio('/ringtone.mp3')
  var interval : any


  function time() {
    if(!ticking) {
      ticking = true
      button.innerHTML = 'Reset Timer'
      interval = setInterval(function() {

        secondsV-=1
        if(secondsV < 10) {
          seconds.innerHTML = `0${secondsV}`
        } else {
          seconds.innerHTML = secondsV
        }

        if(secondsV == 0) {
          if(minutesV == 0) {
            clearInterval(interval)
            ringtone.play()
          } else {
            secondsV = 60
            minutesV-=1 
          }
        }

        minutes.innerHTML = `${minutesV}:`

        console.log(`Minutes: ${minutesV}, Seconds: ${secondsV}`)
      }, 1000)
    }
    else {
      ticking = false
      clearInterval(interval)
      secondsV = 60
      minutesV = 24
      minutes.innerHTML = '25:'
      seconds.innerHTML = '00'
      button.innerHTML = 'Start Timer'
      if(!ringtone.paused) {
        ringtone.currentTime = 0
        ringtone.pause()
      } 
    }
  }
</script>

<main class="w-screen h-screen flex items-center justify-center flex-col bg-black">
  <h1 class="text-white text-6xl font-extrabold">Pomidora</h1>
  <div class="flex">
    <h1 bind:this={minutes} class="text-3xl font-extrabold text-white">25:</h1>
  <h1 bind:this={seconds} class="text-3xl font-extrabold text-white">00</h1>
  </div>

  <div class="flex">
    <button bind:this={breakButton} class="text-white border-white border-2 p-5 rounded-3xl mt-5 w-36 font-extrabold">
      Break
    </button>
  </div>

  <button on:click={()=>time()} bind:this={button} class="text-white border-white border-2 p-5 rounded-3xl mt-8 w-36 font-extrabold">
    Start Timer
  </button>

</main>
