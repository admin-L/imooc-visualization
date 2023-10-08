<template>
  <div
    class="bg-[url('assets/images/bg5.jpg')] bg-cover bg-center h-screen text-white p-5 flex overflow-hidden"
  >
    <div class="flex-1 mr-5 bg-opacity-50 bg-slate-800 p-3 flex flex-col">
      <!-- 横向柱状图 -->
      <HorizontalBar></HorizontalBar>
      <!-- 雷达图 -->
      <RadarBar></RadarBar>
      <!-- 关系图 -->
      <Relation></Relation>
    </div>
    <div class="w-1/2 mr-5 flex flex-col">
      <!-- 数据总览图 -->
      <TotalData></TotalData>
      <!-- 地图可视化 -->
      <MapChart></MapChart>
    </div>
    <div class="flex-1 bg-opacity-50 bg-slate-800 p-3 flex flex-col">
      <!-- 竖向柱状图 -->
      <VerticalBar></VerticalBar>
      <!-- 环形图 -->
      <RingBar></RingBar>
      <!-- 文档云图 -->
      <WordCloud></WordCloud>
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
</script>

<style>
</style>