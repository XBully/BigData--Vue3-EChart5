<template>

  <div>
    <h2>销售总量</h2>
    <div class="chart" id="chart1">
    </div>
  </div>

</template>
  
<script>
import { inject, onMounted, reactive } from "vue"
export default {
  setup() {
    let $echarts = inject("echart")
    let $axios = inject("axios")

    let data = reactive({});
    let xdata = reactive({});
    let ydata = reactive({});

    function setData() {
      xdata = data.data.chartOne.chartData.map(v => v.title);
      ydata = data.data.chartOne.chartData.map(v => v.num);
    }

    async function getState() {
      data = await $axios({ url: "/one/data" })
    }

    onMounted(() => {
      let myChart = $echarts.init(document.getElementById("chart1"));
      getState().then(() => {
        setData();
        myChart.setOption({
          grid:{
            top:"4%",
            left:"1%",
            right:"6%",
            bottom:"3%",
            containLabel:true
          },
          xAxis: {
            type: "value",
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          yAxis: {
            type: "category",
            data: xdata,
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          series: [
            {
              type: "bar",
              data: ydata,
              itemStyle: {
                normal: {
                  barBorderRadius:[0,20,20,0],
                  color: new $echarts.graphic.LinearGradient(0, 0, 1, 0,
                    [{
                      offset: 0,
                      color: "#005eaa"
                    },
                    {
                      offset: .5,
                      color: "#339ca8"
                    },
                    {
                      offset: 1,
                      color: "#cda819"
                    }])
                }
              }
            }
          ]
        })
      });
    })

    return {
      getState, data, xdata, ydata, setData
    }
  }
}
</script>
  
<style scoped>
.chart {
  height: 4.5rem;
}

h2 {
  height: .4rem;
  color: #fff;
  line-height: .6rem;
  font-style: .25rem;
  text-align: center;
}
</style>