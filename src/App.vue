<template>
  <NavAreaComponent @handle-click="requestTracks"/>
  <div style="margin-bottom: 12px"> 
  </div>
  <div style="display:flex; justify-content:center; width:100%">
    <PlaylistArea @selected-track="selectTrack" :tracks="state.tracks" class="w-1/5"/>
    <MainArea :selected-track="state.selectedTrack" class="w-4/5"/>
  </div>
  
</template>

<script setup>
import { reactive } from 'vue';
import MainArea from "./components/MainArea.vue"
import PlaylistArea from "./components/PlaylistArea.vue"
import NavAreaComponent from "./components/NavAreaComponent.vue"
import axios from 'axios'
// import qs from 'qs'



// Replace these values with your client ID and secret
const clientId = import.meta.env.VITE_APP_SPOTIFY_CLIENT_ID
const clientSecret = import.meta.env.VITE_APP_SPOTIFY_CLIENT_SECRET

const encodedAuth = window.btoa(`${clientId}:${clientSecret}`)

const state = reactive({
  tracks: [],
  selectedTrack: {}
})
const selectTrack = ( async (track) => {
  console.log(track)
  state.selectedTrack = track
  //handle select track and playback
})

const requestTracks = ( async (searchText) => {
  // Make the request to get an access token
  await axios.post('https://accounts.spotify.com/api/token', {
      grant_type: 'client_credentials',
    }, {
      headers: {
        Authorization: `Basic ${encodedAuth}`,
        'Content-Type': 'application/x-www-form-urlencoded',
      },
    })
  .then(response => {
    // If the request was successful, the access token will be in the response
    const accessToken = response.data.access_token

    // Use the access token to make a request to search for track names
    axios.get('https://api.spotify.com/v1/search', {
      headers: {
        Authorization: `Bearer ${accessToken}`,
      },
      params: {
        q: searchText,
        type: 'track',
      },
    })
    .then(response => {
      // The response will contain the search results
      
      state.tracks = response.data.tracks.items
      console.log(state.tracks)
    })
    .catch(error => {
      // Handle any errors that occurred in the request
      console.error(error)
    })
  })
  .catch(error => {
    // Handle any errors that occurred in the request
    console.error(error)
  })

})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

