<template>

  <div>
    <h2>库存统计图</h2>
    <div class="chart" id="chart4">
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
      data = await $axios({ url: "/four/data" })
    }
    onMounted(() => {
      let myChart = $echarts.init(document.getElementById("chart4"))
      getState().then(() => {
        myChart.setOption({
          grid:{
            left:"3%",
            right:"4%",
            bottom:"5%",
            containLabel:true
          },
          xAxis:{
            type:"category",
            data:data.data.chartFour.chartData.day,
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          yAxis:{
            type:"value",
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          legend:{
            textStyle:{
              color:"#fff"
            }
          },
          tooltip: {
            trigger: "axis",
            axisPoniter:{
              type:"shadow"
            }
          },
          series: [
            {
              name:"服饰",
              type: "bar",
              data: data.data.chartFour.chartData.num.Chemicals,
              stack:"Total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"数码",
              type: "bar",
              data: data.data.chartFour.chartData.num.Clothes,
              stack:"Total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"家电",
              type: "bar",
              data: data.data.chartFour.chartData.num.Electrical,
              stack:"Total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"家居",
              type: "bar",
              data: data.data.chartFour.chartData.num.digit,
              stack:"Total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"日化",
              type: "bar",
              data: data.data.chartFour.chartData.num.gear,
              stack:"Total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
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
  margin: .15rem;
}
</style>