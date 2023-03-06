<template>
  <div class="dashboardContainer">
    <LocationComponent></LocationComponent>
  </div>
</template>

<script setup lang="ts">
import LocationComponent from './LocationComponent.vue'
</script>

<style lang="scss">
.dashboardContainer {
  width: 1024px;
  background-color: lightgrey;
  border-radius: 4px;
  height: 500px;
}
</style>
