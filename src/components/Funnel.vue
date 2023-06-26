<template>
  <div class="w-[360px] grid grid-cols-2">
    <ul class="col-span-1">
      <li v-for="(item, index) in getItems" @click="items[index].percents = randomPercent()" class="cursor-pointer">
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
  { name: 'Лид', percents: 100, value: 8 },
  { name: 'Сделка', percents: 79, value: 6 },
  { name: 'Эскиз идея', percents: 58, value: 5 },
  { name: 'КП', percents: 54, value: 5 },
  { name: 'КП повтор.', percents: 33, value: 4 },
  { name: 'Договор', percents: 21, value: 2 },
  { name: 'Оплачено', percents: 19, value: 1 },
])

const getItems = computed(() => items.value.sort((a, b) => b.percents - a.percents))

function randomPercent() {
  return Math.floor(Math.random() * (100 - 10 + 1) + 10)
}
</script>

<style>
.funnel-block {
  @apply shrink-0 h-[24px] bg-no-repeat bg-fixed bg-gradient-to-b from-orange-50 from-35% to-orange-900 to-75%;
}
</style>