<template>
  <div class="w-[360px] grid grid-cols-2">
    <ul class="col-span-1" @click="items[0].value = randomPeople()">
      <li v-for="(item, index) in items" class="cursor-pointer">
        {{ index + 1 }}. {{ item.name }}
      </li>
    </ul>
    <div class="col-span-1 space-y-px">
      <div v-for="item in getItems" class="flex justify-center">
        <div class="shrink-0 w-[40px] mr-2 text-right">{{ item.value }}</div>
        <div :style="{ width: `${item.percents / 2}%` }" class="funnel-block rounded-l mr-px"></div>
        <div :style="{ width: `${item.percents / 2}%` }" class="funnel-block rounded-r"></div>
        <div class="shrink-0 w-[40px] ml-2">{{ item.percents }}%</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

const items = ref([
  { name: 'Лид', percents: 100, value: 6 },
  { name: 'Сделка', percents: 0, value: 1 },
  { name: 'Эскиз идея', percents: 0, value: 5 },
  { name: 'КП', percents: 0, value: 3 },
  { name: 'КП повтор.', percents: 0, value:  4 },
  { name: 'Договор', percents: 0, value: 5 },
  { name: 'Оплачено', percents: 0, value: 2 },
])

const getItems = computed(() => {
  items.value.forEach((item, index) => {
    if (index > 0) {
      item.percents = Math.ceil((item.value * 100) / items.value[0].value)
    }
  })

  return [...items.value].sort((a, b) => b.value - a.value)
})

function randomPeople() {
  return Math.floor(Math.random() * (20 - 6 + 1) + 6)
}
</script>

<style>
.funnel-block {
  @apply shrink-0 h-[24px] bg-no-repeat bg-fixed bg-gradient-to-b from-orange-50 from-35% to-slate-500 to-75%;
}
</style>