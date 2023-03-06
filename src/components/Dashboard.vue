<template>
  <div class="dashboardContainer">
    <div v-for="(n, index) in 10" :key="index">
      <LocationComponent></LocationComponent>
    </div>
  </div>
</template>

<script setup lang="ts">
import LocationComponent from './LocationComponent.vue'
</script>

<style lang="scss">
.dashboardContainer {
  width: fit-content;
  background-color: lightgrey;
  border-radius: 4px;
  height: fit-content;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}
</style>
