<template>
  <div>
    <div>大区数据信息</div>
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
console.log(props)

//初始化 echarts 实例
let myChart = null
const target = ref(null)
onMounted(() => {
  myChart = echarts.init(target.value)
  renderChart()
})

//构建 option 配置对象
const renderChart = () => {
  const options = {
    // X 轴数据
    xAxis: {
      show: false,
      type: 'value',
      max: function (value) {
        return parseInt(value.max * 1.2)
      }
    },
    // Y 轴数据
    yAxis: {
      type: 'category',
      data: props.data.regions.map(item => item.name),
      inverse: true,
      axisLine: {
        show: false
      },
      axisTick: {
        show: false
      },
      axisLabel: {
        color: '#9eb1c8'
      }
    },
    // 图标绘制的位置
    grid: {
      top: 0,
      right: 0,
      bottom: 0,
      left: 0,
      containLabel: true,
    },
    series: [
      {
        type: 'bar'
      }
    ]
  }
  myChart.setOption(options)
}
//通过setOption(option) 绑定实例
</script>

<style>
</style>