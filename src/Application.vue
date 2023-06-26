<template>
  <div class="space-y-10">
    <Charts />
    <CircleDiagram class="hidden" />
    <Funnel />
  </div>
</template>

<script setup>
import Charts from './components/Charts.vue'
import CircleDiagram from './components/CircleDiagram.vue'
import Funnel from './components/Funnel.vue'
</script>