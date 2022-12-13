<template>

  <div>
    <h2>库存统计</h2>
    <div class="chart" id="chart3">
    </div>
  </div>

</template>
  
<script>
import { inject, reactive, onMounted } from "vue"

export default {
  setup() {
    let $echarts = inject("echart")
    let $axios = inject("axios")
    let data = reactive({})

    async function getState() {
      data = await $axios({ url: "/three/data" })
    }
    onMounted(() => {
      let myChart = $echarts.init(document.getElementById("chart3"))
      getState().then(() => {
        myChart.setOption({
          legend: {
            top: "bottom",
            textStyle:{
              color:"#fff"
            }
          },
          tooltip: {
            trigger: "item"
          },
          series: [
            {
              type: "pie",
              data: data.data.chartThree.chartData,
              radius: [10, 100],
              center: ["50%", "45%"],
              roseType: "area",
              itemStyle: {
                borderRadius: 10,
              }
            }
          ]
        })
      })
    })
    return {
      data, getState
    }
  }
}

</script>
  
<style scoped>
.chart {
  height: 4.3rem;
}

h2 {
  height: .4rem;
  color: #fff;
  line-height: .6rem;
  font-style: .25rem;
  text-align: center;
}
</style>