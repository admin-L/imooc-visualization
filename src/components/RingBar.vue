<template>
  <div>
    <div>大区异常处理</div>
    <div ref="target" class="w-full h-full"></div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import * as echarts from 'echarts'
const props = defineProps({
  data: {
    type: Object,
    required: true
  }
})

let myChart = null
const target = ref(null)

onMounted(() => {
  myChart = echarts.init(target.value)
  renderChart()
})

const getSeriesData = () => {
  const series = []

  props.data.abnormals.forEach((item, index) => {
    //上层
    series.push({
      name: item.name,
      type: 'pie',
      clockkWise: false,
      hoverAnimation: false,
      radius: [73 - index * 15 + '%', 68 - index * 15 + '%'],
      center: ['55%', '55%'],
      label: {
        show: false
      },
      data: [
        {
          name: item.name,
          value: item.value
        },
        {
          value: 1000,
          itemStyle: {
            color: 'rgba(0,0,0,0)',
            borderWidth: 0
          },
          tooltip: {
            show: false
          },
          hoverAnimation: false
        },
      ]
    })

    series.push({
      name: item.name,
      type: 'pie',
      silent: true,
      z: 1,
      clockWise: false,
      hoverAnimation: false,
      radius: [73 - index * 15 + '%', 68 - index * 15 + '%'],
      center: ['55%', '55%'],
      label: {
        show: false
      },
      data: [
        {
          value: 7.5,
          itemStyle: {
            color: 'rgba(3, 31, 62)',
            borderWidth: 0
          },
          tooltip: {
            show: false,
          },
          hoverAnimation: false
        },
        {
          value: 2.5,
          itemStyle: {
            color: 'rgba(0,0,0,0)',
            borderWidth: 0
          },
          tooltip: {
            show: false,
          },
          hoverAnimation: false
        }
      ]
    })
  })

  //下层
  return series
}

const renderChart = () => {
  const option = {
    //图例配置
    legend: {
      show: true,
      icon: 'circle',
      top: '14%',
      left: '60%',
      data: props.data.abnormals.map(item => item.name),
      width: -5,
      itemWidth: 10,
      itemHeight: 10,
      itemGap: 6,
      textStyle: {
        fontSize: 12,
        lineHeight: 5,
        color: '#ffffff'
      }
    },
    //提示层
    tooltip: {
      show: true,
      trigger: 'item',
      formatter: '{a}<br>{b}:{c}({d}%)'
    },
    //X轴
    xAxis: [
      {
        show: false
      }
    ],
    //Y轴
    yAxis: [
      {
        type: 'category',
        inverse: true,
        axisLine: {
          show: false
        }
      }
    ],
    //核心配置
    series: getSeriesData()
  }

  myChart.setOption(option)
}
watch(() => props.data, () => {
  renderChart()
})
</script>

<style>
</style>