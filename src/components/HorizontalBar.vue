<template>
  <div>
    <div>【大区数据信息】</div>
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

//初始化 echarts 实例
let myChart = null
const target = ref(null)
onMounted(() => {
  myChart = echarts.init(target.value)
  renderChart()
})

//构建 option 配置对象
const renderChart = () => {
  const option = {
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
        type: 'bar',
        data: props.data.regions.map(item => ({
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
          position: 'right',
          textStyle: {
            color: '#ffffff'
          }
        }
      }
    ]
  }
  //通过setOption(option) 绑定实例
  myChart.setOption(option)
}

watch(() => props.data, () => {
  renderChart()
})
</script>

<style>
</style>