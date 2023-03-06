<template>
  <div>yo</div>
</template>

<script setup lang="ts">
import type { Location } from '@/types/Location'

/*const locationExample: Location = {

}*/

const getLocations = async () => {
  fetch('https://alarm-dev.beautycos.dk/Api/Location/GetLocations', {
    method: 'GET'
  })
}
</script>

<style lang="scss"></style>
