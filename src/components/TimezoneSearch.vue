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
const searchResult = $computed(() => {
  return fuse.search(input)
})

function add(t: Timezone) {
  addToTimezone(t)
  input = ''
  index = 0
}

function onKeyDown(e: KeyboardEvent) {
  if (e.key === 'ArrowDown')
    index = (index + 1) % searchResult.length
  else if (e.key === 'ArrowUp')
    index = (index - 1 + searchResult.length) % searchResult.length
  else if (e.key === 'Enter')
    add(searchResult[index].item)
}
</script>

<template>
  <div relative>
    <input
      v-model="input" type="text" placeholder="Search timezone..."
      p="x3 y2" border="~ base rounded" w-full bg-transparent text-xl
      @keydown="onKeyDown"
    >
    <div
      v-show="input"
      border="~ base" bg-base absolute left-0 right-0 top-full max-h-100 overflow-auto p1
    >
      <button
        v-for="i, idx of searchResult"
        :key="i.refIndex" block w-full
        :class="idx === index ? 'bg-gray:10' : ''"
        @click="add(i.item)"
      >
        <TimezoneItem :timezone="i.item" />
      </button>
    </div>
  </div>
</template>
