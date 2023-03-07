<template>
  <div class="dashboardContainer">
    <div v-for="(location, index) in locations" :key="index">
      <LocationComponent
        :location="location"
        :alarm-active="location.alarmActive"
        @toggle-alarm="location.alarmActive = $event"
      ></LocationComponent>
    </div>
  </div>
</template>

<script setup lang="ts">
import LocationComponent from './LocationComponent.vue'
import type { Location } from '@/types/Location'
import { computed, ref } from 'vue'

let locations = ref<Location[]>()

fetch('/Api/Location/GetLocations', {
  method: 'GET',
  headers: {
    XApiKey: import.meta.env.VITE_API_KEY
  }
})
  .then((response) => response.json())
  .then((data) => {
    locations.value = data
    locations.value?.push({
      uuid: '1',
      lastAlarm: '000',
      name: 'hej',
      alarmActive: true
    })
    console.log(locations.value)
  })
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
