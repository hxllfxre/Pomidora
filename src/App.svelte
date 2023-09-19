<script lang="ts">
    import { tick } from "svelte";

  let button : any
  let ticking : Boolean = false
  let minutes : any
  let seconds : any
  let secondsV = 60
  let minutesV = 24
  let breakButton : any
  let mode = 'Focus'
  let main : any
  var ringtone = new Audio('/ringtone.mp3')
  var interval : any
  var h1Elements = document.getElementsByTagName("h1");

  function blackButtons() {
    button.style.color = 'black'
    button.style.borderColor = 'black'
    breakButton.style.color = 'black'
    breakButton.style.borderColor = 'black'
  }
  function whiteButtons() {
    button.style.color = 'white'
    button.style.borderColor = 'white'
    breakButton.style.color = 'white'
    breakButton.style.borderColor = 'white'
  }
  function blackHeaders() {
    for(var i = 0; i < h1Elements.length; i++) {
      h1Elements[i].style.color = 'black'
    }
  }
  function whiteHeaders() {
    for(var i = 0; i < h1Elements.length; i++) {
      h1Elements[i].style.color = 'white'
    }
  }

  function switchTheme(clickedId : String) {
    console.log(clickedId)
    switch(clickedId) {
      case 'blue':
        main.style.backgroundColor = '#9efdef' 
        blackHeaders()
        blackButtons()
      break
      case 'pink':
        main.style.backgroundColor = '#df83ff'
        blackHeaders()
        blackButtons()
      break
      case 'light':
        main.style.backgroundColor = 'white'
        blackHeaders()
        blackButtons()
      break
      case 'dark':
        main.style.backgroundColor = 'black'
        whiteHeaders()
        whiteButtons()
      break
    }
  }

  function switchMode() {
    if(mode == 'Break') {
      mode = 'Focus'
      minutes.innerHTML = '25:'
      breakButton.innerHTML = 'Focus'
    } else if(mode == 'Focus') {
      mode = 'Break'
      minutes.innerHTML = '5:'
      breakButton.innerHTML = 'Break'
    }
  }

  function time() {
    if(!ticking) {
      ticking = true
      button.innerHTML = 'Reset Timer'

      if(mode == 'Break') {
        minutesV = 4
        secondsV = 60
      } else {
        minutesV = 24
        secondsV = 60
      }

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
        console.log(`Mode: ${mode}`)
      }, 1000)
    }
    else {
      ticking = false
      clearInterval(interval)
      if(mode == 'Focus') {
        secondsV = 60
        minutesV = 24
        minutes.innerHTML = '25:'
      } else {
        secondsV = 60
        minutesV = 4
        minutes.innerHTML = '5:'
      }

      seconds.innerHTML = '00'
      button.innerHTML = 'Start Timer'

      if(!ringtone.paused) {
        ringtone.currentTime = 0
        ringtone.pause()
      } 
    }
  }
</script>

<main bind:this={main} class="w-screen h-screen flex items-center justify-center flex-col bg-black">
  <h1 class="text-white text-6xl font-extrabold">Pomidora</h1>
  <div class="flex">
    <h1 bind:this={minutes} class="text-3xl font-extrabold text-white">25:</h1>
  <h1 bind:this={seconds} class="text-3xl font-extrabold text-white">00</h1>
  </div>

  <div class="flex">
    <button bind:this={breakButton} on:click={()=>switchMode()} class="text-white border-white border-2 p-5 rounded-3xl mt-5 w-36 font-extrabold">
      Break
    </button>
  </div>

  <button on:click={()=>time()} bind:this={button} class="text-white border-white border-2 p-5 rounded-3xl mt-8 w-36 font-extrabold">
    Start Timer
  </button>

  <div class="flex flex-nowrap bottom-0 right-0 absolute p-5 gap-2">
    <button on:click={()=>switchTheme('light')} class="w-8 h-8 bg-white rounded-xl"></button>
    <button on:click={()=>switchTheme('dark')} class="w-8 h-8 bg-gray-800 rounded-xl"></button>
    <button on:click={()=>switchTheme('pink')} class="w-8 h-8 bg-pink-500 rounded-xl"></button>
    <button on:click={()=>switchTheme('blue')} class="w-8 h-8 bg-blue-300 rounded-xl"></button>
  </div>

</main>
