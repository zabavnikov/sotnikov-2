<template>
  <div class="w-[1024px] h-[360px] p-10">
    <VChart :option="option" autoresize />
  </div>
</template>

<script setup>
import * as echarts from 'echarts'
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import { LineChart } from 'echarts/charts'
import {
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  GridComponent,
} from 'echarts/components'
import VChart from 'vue-echarts'
import { ref } from 'vue'

use([
  CanvasRenderer,
  LineChart,
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  GridComponent,
])

const option = ref({
  color: ['#4F46E5', '#AE1AC6'],
  title: {
    text: 'Динамика'
  },
  tooltip: {
    trigger: 'item',
    position: 'top',
    axisPointer: {
      type: 'cross',
      label: {
        backgroundColor: '#6a7985'
      }
    },
    padding: 0,
    borderRadius: 12,

    formatter: (params) => {
      return `
        <div class="p-4">
          <div class="text-center text-gray-500 mb-2">${params.data.name}</div>
          <div class="flex items-center mb-2">
            <div class="font-bold mr-4">${params.data.price}</div>
            <div class="bg-red-700 px-2 rounded-full text-white text-xs">${params.data.down}%</div>
          </div>
          <div class="flex justify-between text-xs mb-1">
            <div>75,000</div>
            <div class="text-orange-500">64%</div>
          </div>
          <div class="h-2 bg-slate-100">
            <div class="h-full bg-orange-500" style="width: 64%"></div>
          </div>
        </div>
      `
    }
  },
  legend: {
    data: ['План', 'Факт 1']
  },
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: [
    {
      type: 'category',
      boundaryGap: false,
      data: ['Фев', 'Мар', 'Апр', 'Май', 'Июн', 'Июл', 'Авг'],
    }
  ],
  yAxis: [
    {
      type: 'value',
      axisLabel: {
        formatter: '{value}Р'
      }
    }
  ],
  series: [
    {
      type: 'bar',
      data: [75_000, 75_000, 75_000, 75_000, 75_000, 75_000, 75_000],
      barWidth: '8px',
      itemStyle: {
        color: '#4FCBCB'
      },
      tooltip: {
        show: false,
      }
    },
    {
      name: 'План',
      type: 'line',
      smooth: true,
      lineStyle: {
        width: 2
      },
      showSymbol: false,
      emphasis: {
        focus: 'series'
      },
      data: [
        { value: 45_591, name: 'Июнь 2023', price: '45,591Р', down: 4 },
        { value: 5_591, name: 'Июнь 2023', price: '5,591Р', down: 1 },
        { value: 35_591, name: 'Июнь 2023', price: '35,591Р', down: 1 },
        { value: 95_591, name: 'Июнь 2023', price: '95,591Р', down: 8 },
        { value: 75_591,  name: 'Июнь 2023', price: '75,591Р', down: 24 },
        { value: 25_591, name: 'Июнь 2023', price: '25,591Р', down: 12 },
        { value: 15_591, name: 'Июнь 2023', price: '15,591Р', down: 9 },
      ],
      symbolSize: 12,
    },
    {
      name: 'Факт 1',
      type: 'line',
      smooth: true,
      lineStyle: {
        width: 2
      },
      showSymbol: false,
      emphasis: {
        focus: 'series'
      },
      data: [
        { value: 42_591, name: 'Июнь 2023', price: '45,591Р',  down: 4 },
        { value: 2_591, name: 'Июнь 2023', price: '5,591Р',   down: 1 },
        { value: 32_591,  name: 'Июнь 2023', price: '35,591Р',  down: 1 },
        { value: 92_591, name: 'Июнь 2023', price: '95,591Р',  down: 8 },
        { value: 72_591,  name: 'Июнь 2023', price: '75,591Р', down: 24 },
        { value: 22_591, name: 'Июнь 2023', price: '25,591Р',  down: 12 },
        { value: 12_591, name: 'Июнь 2023', price: '15,591Р',  down: 9 },
      ],
      areaStyle: {
        opacity: 0.2,
        color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          {
            offset: 0,
            color: 'rgba(174, 26, 198, 1)'
          },
          {
            offset: 1,
            color: 'rgba(253, 237, 255, 0.5)'
          }
        ])
      },
      symbolSize: 12
    }
  ]
})
</script>
