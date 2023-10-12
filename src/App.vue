<template>
  <div
    class="bg-[url('assets/images/bg5.jpg')] bg-cover bg-center h-screen text-white p-5 flex overflow-hidden"
    v-if="data"
  >
    <div class="flex flex-col flex-1 p-3 mr-5 bg-opacity-50 bg-slate-800">
      <!-- 横向柱状图 -->
      <HorizontalBar class="box-border pb-4 h-1/3" :data="data.regionData"></HorizontalBar>
      <!-- 雷达图 -->
      <RadarBar class="box-border pb-4 h-1/3" :data="data.riskData"></RadarBar>
      <!-- 关系图 -->
      <Relation class="h-1/3"></Relation>
    </div>
    <div class="flex flex-col w-1/2 mr-5">
      <!-- 数据总览图 -->
      <TotalData class="p-3 bg-opacity-50 bg-slate-800"></TotalData>
      <!-- 地图可视化 -->
      <MapChart class="flex-1 p-3 mt-4 bg-opacity-50 bg-slate-800"></MapChart>
    </div>
    <div class="flex flex-col flex-1 p-3 bg-opacity-50 bg-slate-800">
      <!-- 竖向柱状图 -->
      <VerticalBar class="box-border pb-4 h-1/3" :data="data.serverData"></VerticalBar>
      <!-- 环形图 -->
      <RingBar class="box-border pb-4 h-1/3" :data="data.abnormalData"></RingBar>
      <!-- 文档云图 -->
      <WordCloud class="h-1/3"></WordCloud>
    </div>
  </div>
</template>

<script setup>
import HorizontalBar from "./components/HorizontalBar.vue";
import MapChart from "./components/MapChart.vue";
import RadarBar from "./components/RadarBar.vue";
import Relation from "./components/Relation.vue";
import RingBar from "./components/RingBar.vue";
import TotalData from "./components/TotalData.vue";
import VerticalBar from "./components/VerticalBar.vue";
import WordCloud from "./components/WordCloud.vue";

import { ref } from 'vue'

import { getVisualization } from './api/visualization.js'

const data = ref(null)
const loadData = async () => {
  data.value = await getVisualization()
  // console.log(data.value)
}
setInterval(() => {
  loadData()
}, 3000)
</script>

<style>
</style>