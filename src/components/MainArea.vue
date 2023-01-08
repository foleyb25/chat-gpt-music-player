<template>
    <div class="h-screen p-4 bg-[#333] bg-gradient-to-b from-[rgba(0,0,0,0.5)] to-[rgba(0,0,0,0)]">
      <div id="album-cover" class=" h-3/5 flex items-center p-[20px]" v-if="selectedTrack.album">
        <img class="w-full" :src="selectedTrack.album.images[0].url" alt="Album artwork">
      </div>
      <div id="track-details" class="h-1/5">
        <div class="ml-[20px]">
          <h1 class="text-[2em] text-[#fff] m-0">{{ selectedTrack.name }}</h1>
          <h2 v-if="selectedTrack.artists" class="text-[1.5em] text-[#ccc] m-0">{{ selectedTrack.artists[0].name }}</h2>
        </div>
      </div>
      <div class="h-1/5 flex items-center py-0 px-[20px]">
        <input class="slide-style w-full h-[5px] bg-[#ddd] rounded" type="range" v-model="currentTime" :max="duration" @input="seekTrack">
        <div class="ml-[20px] text-[#fff]">
            {{ formattedCurrentTime }} / {{ formattedDuration }}
        </div>
      </div>
    </div>
    
</template>
  
  <script>
  export default {
    props: ['selectedTrack'],
    data() {
      return {
        track: {
          title: '',
          artist: '',
          artwork: ''
        },
        currentTime: 0,
        duration: 0
      }
    },
    methods: {
      seekTrack(event) {
        // Seek to the selected time in the track
        this.currentTime = event.target.value
      },
      formatTime(time) {
        // Format the time as a string in the format "MM:SS"
        const minutes = Math.floor(time / 60)
        const seconds = time % 60
        return `${minutes}:${seconds.toString().padStart(2, '0')}`
        }
    },
    computed: {
        formattedCurrentTime() {
      // Format the current time as a string in the format "MM:SS"
      return this.formatTime(this.currentTime)
        },
        formattedDuration() {
        // Format the duration as a string in the format "MM:SS"
        return this.formatTime(this.duration)
        }
    }
  }
  </script>
  
  <style>


/* Style the range input */
.slide-style {
  -webkit-appearance: none;
}

.slide-style[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  background-color: #fff;
  border-radius: 50%;
  cursor: pointer;
}

.slide-style[type="range"]:focus {
  outline: none;
}

  </style>
  