<script setup lang="ts">
import type { Timezone } from '../types'

const { timezone } = defineProps<{
  timezone: Timezone
}>()

const state = $computed(() => timezone.name.split('/')[0])
const city = $computed(() => timezone.name.split('/')[1])
const offset = $computed(() => timezone.offset > 0 ? `+${timezone.offset}` : timezone.offset)
</script>

<template>
  <div flex gap2 py1>
    <div ma w-8 font-bold op80>
      {{ offset }}
    </div>
    <div flex="~ col" flex-auto text-left>
      <div>
        {{ city }}
      </div>
      <div text-sm leading-1em op50>
        {{ state }}
      </div>
    </div>
  </div>
</template>
