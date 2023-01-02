<template>
    <nav class="flex items-center justify-between bg-[#333] bg-gradient-to-b from-[rgba(0,0,0,0.5)] to-[rgba(0,0,0,0)]">
      <ul class="list-none flex">
        <li v-for="item in state.items" :key="item.text" class="my-[10px] mx-[10px]">
          <router-link :to="item.path" class="hover:text-[#fff] text-[#ccc] decordation-none text-[1.5em]">{{ item.text }}</router-link >
        </li>
      </ul>
      <button style="background-color:lightcoral" @click="$emit('handleClick', state.searchText)">Search tracks</button>
      <input style="margin-left: 8px;" type="text" v-model="state.searchText">
    </nav>
  </template>
  
  <script setup>

  import {reactive} from "vue"

  const state = reactive({
    items: [
          { text: 'Home', path: '/' },
          { text: 'Discover', path: '/discover' },
          { text: 'Library', path: '/library' }
        ]
  })
  </script>
  