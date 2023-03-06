<template>
  <div class="dashboardContainer">
    <div v-for="(location, index) in locationExamples" :key="index">
      <LocationComponent
        :location-example="location"
        :border-alarm-color="triggerAlarm(location)"
      ></LocationComponent>
    </div>
  </div>
</template>

<script setup lang="ts">
import LocationComponent from './LocationComponent.vue'
import type { Location } from '@/types/Location'
import { computed } from 'vue'

const locationAlarms: Location[] = [
  {
    uuid: '2a3e4f8d-9786-4c7b-b47e-4fa8f915194c',
    name: 'Kolding - Jernbanegade',
    lastAlarm: '2023-03-06T09:03:35.4039083Z'
  }
]
const triggerAlarm = (location: Location): string => {
  let abc: string = ''
  locationAlarms.forEach((locationAlarm) =>
    locationAlarm.uuid == location.uuid ? (abc = ' red') : (abc = ' black')
  )
  /*
  disabled untill needed
  var audio = new Audio('public/warning.mp3')
  audio.play()*/

  return abc
}
const locationExamples: Location[] = [
  {
    uuid: '2a3e4f8d-9786-4c7b-b47e-4fa8f915194c',
    name: 'Kolding - Jernbanegade',
    lastAlarm: '2023-03-06T09:03:35.4039083Z'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  },
  {
    uuid: '2a3e4f8d-9786-4c7b-b47e-4fa8f915194c',
    name: 'Kolding - Jernbanegade',
    lastAlarm: '2023-03-06T09:03:35.4039083Z'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  },
  {
    uuid: '244894e0-01e0-480e-88f1-01305bdadabf',
    name: 'Roskilde - Algade',
    lastAlarm: 'Never triggered'
  }
]
</script>

<style lang="scss">
.dashboardContainer {
  display: inline-grid;
  grid-template-columns: repeat(2, 1fr);
  background-color: lightgrey;
  white-space: nowrap;
  border-radius: 4px;
  @media (max-width: 869px) {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
