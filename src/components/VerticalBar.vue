<template>
  <div>
    <div>服务资源占用比</div>
    <div ref="target" class="w-full h-full"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import * as echarts from 'echarts'
const props = defineProps({
  data: {
    type: Object,
    required: true
  }
})
console.log(props.data)

const myChart = null
const target = ref(null)

// onMounted(() => {
//   myChart = echarts.init(target.value)
//   // renderChart()
// })

const renderChart = () => {
  const option = {
    xAxis: {
      type: 'category'
    },
    yAxis: {},
    grid: {},
    series: []
  }

  myChart.setOption(option)
}
</script>
<style>
</style>