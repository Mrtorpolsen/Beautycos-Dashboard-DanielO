<template>
  <div class="dashboardContainer">
    <div v-for="(location, index) in locations" :key="index">
      <Suspense>
        <LocationComponent
          :location="location"
          :alarm-active="(location.alarmActive as boolean)"
          @update:toggle-alarm="location.alarmActive = $event"
          @update:location="getLocations"
        ></LocationComponent>
      </Suspense>
    </div>
  </div>
</template>

<script setup lang="ts">
import LocationComponent from './LocationComponent.vue'
import type { Location } from '@/types/Location'
import { onMounted, onUnmounted, ref } from 'vue'

const locations = ref<Location[]>()
const UtcTime = ref<string>()
const alarmActiveLocations = ref<Location[]>()
const interval = ref<number>()

const getUtcTime = async () => {
  try {
    const response = await fetch('/Api/Location/GetUtcNow', {
      method: 'GET',
      headers: {
        XApiKey: import.meta.env.VITE_API_KEY
      }
    })
    const result = await response.json()
    UtcTime.value = result
  } catch (e) {
    console.error(e)
  }
}

//Should use transform and set alarmLocation to false, and also check if name is null.
//This way i wont have to do it in Location
const getLocations = async () => {
  try {
    const response = await fetch('/Api/Location/GetLocations', {
      method: 'GET',
      headers: {
        XApiKey: import.meta.env.VITE_API_KEY
      }
    })
    const data = await response.json()

    locations.value = data
  } catch (e) {
    console.error(e)
  }
}
const lisentForAlarm = async () => {
  try {
    if (UtcTime.value == undefined) {
      await getUtcTime()
    }

    const response = await fetch('/Api/Location/LongPull?last_pull=' + UtcTime.value, {
      method: 'POST',
      headers: {
        XApiKey: import.meta.env.VITE_API_KEY,
        'Content-Type': 'application/json; charset=utf-8'
      }
    })
    const data = await response.json()
    //Need to look into this, so that multiple alarms can be active at once.
    //sets alarm active to true, if a match is found in alarmActiveLocations
    alarmActiveLocations.value = data.locations
    locations.value?.map(
      (location) =>
        (location.alarmActive = alarmActiveLocations.value?.some(
          (alarmActiveLocation) => location.uuid == alarmActiveLocation.uuid
        ))
    )
    //updates pull time
    UtcTime.value = data.nextLastPull

    console.log(data)
  } catch (e) {
    console.error(e)
  }
}

onMounted(() => {
  getLocations()

  lisentForAlarm()

  interval.value = setInterval(lisentForAlarm, 5000)
})

onUnmounted(() => clearInterval(interval.value))
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
