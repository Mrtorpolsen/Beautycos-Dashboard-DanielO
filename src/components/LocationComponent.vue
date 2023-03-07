<template>
  <div class="locationContainer">
    <div class="locationContent">
      <div>Location : {{ props.location.name }}</div>
      <div>Last Alarm : {{ props.location.lastAlarm }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Location } from '@/types/Location'
import { ref } from 'vue'

const props = defineProps<{
  location: Location
  alarmActive: boolean
}>()
</script>

<style lang="scss">
.locationContainer {
  display: flex;
  flex-direction: column;
  border: solid;
  align-items: start;
  margin: 8px 6px 8px 6px;
  border-radius: 4px;
  background-color: rgb(242, 242, 242);
}
.locationContent {
  padding: 6px;
}
</style>
