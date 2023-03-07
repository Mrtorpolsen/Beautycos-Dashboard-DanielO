<template>
  <div class="locationContainerAlarm" v-if="toggleAlarm" @click="toggleAlarm = false">
    <div class="locationContent">
      <div>Location : {{ props.location.name }}</div>
      <div>Last Alarm : {{ props.location.lastAlarm }}</div>
    </div>
  </div>
  <div class="locationContainer" v-else>
    <div class="locationContent">
      <div>Location : {{ props.location.name }}</div>
      <div>Last Alarm : {{ props.location.lastAlarm }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Location } from '@/types/Location'
import { computed, ref } from 'vue'

const props = defineProps<{
  location: Location
  alarmActive: boolean
}>()

const emit = defineEmits(['toggleAlarm'])

const toggleAlarm = computed({
  get: () => props.alarmActive ?? false,
  set: () => {
    emit('toggleAlarm', false)
  }
})
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
.locationContainerAlarm {
  display: flex;
  flex-direction: column;
  border: solid;
  border-color: red;
  align-items: start;
  margin: 8px 6px 8px 6px;
  border-radius: 4px;
  background-color: rgb(242, 242, 242);
  cursor: pointer;
  animation-name: stretch;
  animation-duration: 2s;
  animation-timing-function: ease-out;
  animation-direction: alternate;
  animation-iteration-count: infinite;
  animation-play-state: running;
}
@keyframes stretch {
  0% {
    transform: scale(1);
  }

  100% {
    transform: scale(1.1);
  }
}
.locationContent {
  padding: 6px;
}
</style>
