<script setup lang="ts">
import Fuse from 'fuse.js'
import type { Timezone } from '../types'
import { timezones } from '../composoables/data'
import { addToTimezone } from '../composoables/state'

const fuse = new Fuse(timezones, {
  keys: ['name'],
})

let input = $ref('')
let index = $ref(0)
const searchResult = computed(() => {
  return fuse.search(input)
})

function add(t: Timezone) {
  addToTimezone(t)
  input = ''
  index = 0
}
</script>

<template>
  <div relative>
    <input
      v-model="input"
      type="text"
      placeholder="Search timezone..."
      border="~ gray/15 rounded"
      w-full bg-transparent px2 py1
    >
    <div v-show="input" absolute left-0 right-0 top-full bg-gray-900>
      <button
        v-for="i of searchResult"
        :key="i.refIndex"
        flex gap2
        @click="add(i.item)"
      >
        <div w-10 text-right font-mono>
          {{ i.item.offset }}
        </div>
        <div>
          {{ i.item.name }}
        </div>
      </button>
    </div>
  </div>
</template>
