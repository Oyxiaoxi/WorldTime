<script setup lang="ts">
</script>

<template>
  <div bg-canvas h-screen font-sans>
    <Navbar />
    <div border="~ base rounded" bg-base m2 shadow>
      <ActionBar />
      <TimeSchedular />
    </div>
  </div>
</template>

<style>
html.dark {
  background: #222;
  color: white;
  color-scheme: dark;
}
</style>
