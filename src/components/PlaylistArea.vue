<template>
    <div class="bg-[#333] bg-gradient-to-b from-[rgba(0,0,0,0.5)] to-[rgba(0,0,0,0)]">
      <ul class="list-none m-0 p-0">
        <li v-for="track in tracks" :key="track.id" @click="selectTrack(track)" class="
        flex items-center p-[20px] cursor-pointer hover:bg-black hover:bg-opacity-[0.1]">
          <img class="w-[20%]" v-if="track.album.images[0]" :src="track.album.images[0].url" alt="Album artwork">
          <div class="ml-[20px]">
            <!-- {{track}} -->
            <h1 class="text-[1.5em] text-[#fff] m-0">{{ track.name }}</h1> 
            <h2 class="text-[1.25em] text-[#ccc] m-0">{{ track.artists[0].name  }}</h2>
            <h3>{{ `${(Math.floor(track.duration_ms / 1000 / 60))}m ${Math.floor(((track.duration_ms / 1000) % 60))}s` }}</h3>
            <h3>{{ track.name }}</h3> 
          </div>
        </li>
      </ul>
    </div>
  </template>



  <script>
  export default {
    props: {
      tracks: {
        type:Array,
        required: true
      }
    },
    data() {
      return {
        state: ""
      }
    },
    methods: {
      selectTrack(track) {
        // Select the track and start playback
        this.$emit('selected-track', track)
      }
    }
  }
  </script>