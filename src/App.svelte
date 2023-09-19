<script lang="ts">
  let button : any
  let timer
  let ticking : Boolean = false
  let minutes : any
  let seconds : any
  let secondsV = 30
  let minutesV = 0
  var ringtone = new Audio('/ringtone.mp3')
  var interval : any

  function theTimer() { 
        secondsV-=1
        if(secondsV < 10) {
          seconds.innerHTML = `0${secondsV}`
        } else {
          seconds.innerHTML = secondsV
        }

        if(secondsV == 0) {
          secondsV = 60
          minutesV-=1
        }
        minutes.innerHTML = `${minutesV}:`

        // check if all time has passed
        if(minutesV === 0 && secondsV === 0) {
          ringtone.play()
          interval = setInterval(theTimer, 4000)
          clearInterval(interval)
        }
  }

  function time() {
    if(seconds.innerHTML == '00') {
      button.innerHTML = 'Reset Timer'
      interval = setInterval(theTimer, 1000)
    }
    else {
      clearInterval(interval)
      secondsV = 60
      minutesV = 24
      minutes.innerHTML = '25:'
      seconds.innerHTML = '00'
      button.innerHTML = 'Start Timer'
    }
  }
</script>

<main class="w-screen h-screen flex items-center justify-center flex-col bg-black">
  <h1 class="text-white text-6xl font-extrabold">Pomidora</h1>
  <div class="flex">
    <h1 bind:this={minutes} class="text-3xl font-extrabold text-white">25:</h1>
  <h1 bind:this={seconds} class="text-3xl font-extrabold text-white">00</h1>
  </div>
  <button on:click={()=>time()} bind:this={button} class="text-white border-white border-2 p-5 rounded-3xl mt-14">
    Start Timer
  </button>
</main>
