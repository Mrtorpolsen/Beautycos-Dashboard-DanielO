<template>
  <div class="locationContainer" :style="{ borderColor: props.borderAlarmColor }">
    <div class="locationContent">
      <div>Location : {{ props.locationExample.name }}</div>
      <div>Last Alarm: {{ props.locationExample.lastAlarm }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Location } from '@/types/Location'
import { ref } from 'vue'

const props = defineProps<{
  locationExample: Location
  borderAlarmColor: string
}>()

console.log(props.borderAlarmColor)

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
  border-radius: 4px;
  background-color: rgb(242, 242, 242);
}
.locationContent {
  padding: 6px;
}
</style>
