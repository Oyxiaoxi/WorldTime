<script setup lang="ts">
import { moveZone, removeZone, zones } from '~/composoables/state'
</script>

<template>
  <div>
    <div v-for="zone, idx of zones" :key="zone.name" border="b base" relative px4 py2>
      <TimezoneItem :timezone="zone" />
      <div
        left="-6"
        flex="~ col" absolute bottom-0 top-0 justify-center text-xl
      >
        <button
          i-carbon-close m--1px icon-btn
          title="Remove"
          @click="removeZone(zone)"
        />
        <button
          v-if="idx !== 0"
          i-carbon-caret-up m--1px icon-btn
          title="Move up"
          @click="moveZone(zone, -1)"
        />
        <button
          v-if="idx !== zones.length - 1"
          i-carbon-caret-down m--1px icon-btn
          title="Move down"
          @click="moveZone(zone, 1)"
        />
      </div>
    </div>
  </div>
</template>
