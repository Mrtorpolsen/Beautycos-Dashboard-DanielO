<template>
  <div class="locationContainer">
    <div class="locationContent">
      <div>Location : {{ locationExample.name }}</div>
      <div>Last Alarm: 2023-03-06T09:03:35.4039083Z</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Location } from '@/types/Location'
import { ref } from 'vue'

const locationExample: Location = {
  uuid: '2a3e4f8d-9786-4c7b-b47e-4fa8f915194c',
  name: 'Kolding - Jernbanegade',
  lastAlarm: 'Never triggered'
}

const test = ref()
/*

console.log(test.value)

fetch(import.meta.env.VITE_API_GET_URL, {
  method: 'GET',
  headers: {
    Authorization: 'XApiKey: ' + import.meta.env.VITE_API_KEY
  }
})
  .then((response) => response.json())
  .then((data) => (test.value = data))
  */
</script>

<style lang="scss">
.locationContainer {
  display: flex;
  flex-direction: column;
  border: solid;
  align-items: center;
  margin: 8px 6px 8px 6px;
}
.locationContent {
  padding: 6px;
}
</style>
