<template>
  <section class="grid grid-cols-6 gap-4 w-[640px]">
    <div class="col-span-2 bg-slate-100">
      <canvas></canvas>
    </div>
    <div class="col-span-4 bg-slate-100"></div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'

const items = [
  { name: 'Эдуард Страженский', percents: 17 },
  { name: 'Разенкова Елена', percents: 9 },
  { name: 'Акименко Александр', percents: 30 },
  { name: 'Иван Иванов', percents: 13 },
  { name: 'Петр Петров', percents: 29 },
]

onMounted(() => {
  const canvas = document.querySelector('canvas')
})
</script>