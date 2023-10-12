<template>
  <div>
    <div>【服务资源占用比】</div>
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

const renderChart = () => {
  const option = {
    xAxis: {
      type: 'category',
      data: props.data.servers.map(item => item.name),
      axisLabel: {
        color: '#9eb1c8'
      }
    },
    yAxis: {
      type: 'value',
      show: false,
      max: function (value) {
        return parseInt(value.max * 1.2)
      }
    },
    grid: {
      top: 16,
      right: 0,
      bottom: 26,
      left: -26,
      containLabel: true
    },
    series: [
      {
        type: 'bar',
        data: props.data.servers.map(item => ({
          name: item.name,
          value: item.value
        })),
        showBackground: true,
        backgroundStyle: {
          color: 'rgba(180, 180, 180, 0.2)'
        },
        itemStyle: {
          color: '#4d9ad3',
          barBorderRadius: 5,
          shadowColor: 'rgba(0, 0, 0, 0.3)',
          shadowBlur: 5
        },
        barWidth: 12,
        label: {
          show: true,
          position: 'top',
          textStyle: {
            color: '#ffffff'
          },
          formatter: '{c}%'
        }
      }
    ]
  }

  myChart.setOption(option)
}
watch(() => props.data, () => {
  renderChart()
})
</script>
<style>
</style>