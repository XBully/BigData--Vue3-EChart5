<template>
  <router-view/>
</template>
<script setup>
import {provide} from "vue"
import * as echarts from "echarts"
import axios from "axios"

//设置基准路径
axios.defaults.baseURL="http://localhost:8888"

provide("echart",echarts)
provide("axios",axios)

</script>

<style lang="less">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    background: url("./assets/bg.jpeg") top  center no-repeat;
    background-size: 1920px 1080px;
  }
</style>
