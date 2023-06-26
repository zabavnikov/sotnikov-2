<template>
  <section class="grid grid-cols-4 gap-4">
    <div class="bg-slate-100 p-4">
      <ul>
        <li
          v-for="user in users"
          @click="user.disabled = !user.disabled"
          class="flex items-center space-x-2 cursor-pointer"
          :class="{'line-through': !!user.disabled}"
        >
          <span class="w-4 h-4 rounded-full" :style="{ backgroundColor: user.color }"></span>
          <span>{{ user.name }}</span>
        </li>
      </ul>
    </div>
    <div class="col-span-2 bg-slate-100 p-4">
      <Line :data="{ labels: lineLabels, datasets: lineDatasets }" :options="{ responsive: true, maintainAspectRatio: false }" />
    </div>
    <div class="bg-slate-100 p-4">
      <Pie :data="{ labels: pieLabels, datasets: pieDatasets }" :options="{ responsive: true, maintainAspectRatio: false }" />
    </div>
  </section>
</template>

<script setup>
import {
  Chart as ChartJS,
  ArcElement,
  Title,
  Tooltip,
  Legend,
  PointElement,
  LineElement,
  BarElement,
  CategoryScale,
  LinearScale,
} from 'chart.js'
import { Pie, Line } from 'vue-chartjs'
import { ref, computed } from 'vue'
import { format, eachDayOfInterval } from 'date-fns'

ChartJS.register(
  ArcElement,
  BarElement,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend,
)

const users = ref([
  { name: 'Эдуард Страженский', percents: 17, disabled: false, color: '#41b883', },
  { name: 'Разенкова Елена', percents: 9, disabled: false, color: '#0a79d3', },
  { name: 'Акименко Александр', percents: 30, disabled: false, color: '#00d8ff', },
  { name: 'Иван Иванов', percents: 13, disabled: false, color: '#dd1b16', },
  { name: 'Петр Петров', percents: 29, disabled: false, color: '#51dc22', },
])

const pieLabels = computed(() => {
  return users.value.filter((user) => user.disabled === false)
    .map((user) => user.name)
})

const pieDatasets = computed(() => {
  const options = {
    backgroundColor: [],
    data: [],
  }

  users.value.forEach((user) => {
    if (user.disabled === false) {
      options.backgroundColor.push(user.color)
      options.data.push(user.percents)
    }
  })

  return [options]
})

const lineLabels = eachDayOfInterval(
{ start: new Date(2014, 9, 1), end: new Date(2014, 9, 31)})
  .map((date) => format(date, 'dd.MM.yyyy')
)

const lineDatasets = computed(() => {
  const options = []

  users.value.forEach((user) => {
    if (user.disabled === false) {
      options.push({
        label: user.name,
        backgroundColor: user.color,
        data: lineLabels.map(() => randomPercent())
      })
    }
  })

  return options
})

function randomPercent() {
  return Math.floor(Math.random() * (100 - 10 + 1) + 10)
}
</script>