<template>

<div>
  <h2>周销图</h2>
  <div class="chart" id="chart2">
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
      data = await $axios({ url: "two/data" })
    }
    onMounted(() => {
      let myChart = $echarts.init(document.getElementById("chart2"))
      getState().then(() => {
        myChart.setOption({
          tooltip:{
            trigger:"axis",
            axisPonit:{
              type:"cross",
              label:{
                backgroundColor:"#e6b600"
              }
            }
          },
          legend:{
            data:["服饰","数码","家电","家居","日化"],
            textStyle:{
              color:"#fff"
            }
          },
          grid:{
            left:"1%",
            right:"4%",
            bottom:"3%",
            containLabel:true
          },
          xAxis:{
            type:"category",
            boundaryGap:false,
            data:data.data.chartTwo.chartData.day,
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
          series: [
            {
              name:"服饰",
              type: "line",
              data: data.data.chartTwo.chartData.num.Chemicals,
              smooth:true,
              showSymbol:false,
              stack:"Total",
              lineStyle:{
                width:0
              },
              emphasis:{
                focus:"series"
              },
              areaStyle:{
                opacity:.8,
                color:new $echarts.graphic.LinearGradient(0,0,0,1,[
                  {
                  offset:0,
                  color:"rgba(128,255,165)"
                  },
                  {
                  offset:1,
                  color:"rgba(1,191,236)"
                  },
              ])
              }
            },
            {
              name:"数码",
              type: "line",
              data: data.data.chartTwo.chartData.num.Clothes,
              smooth:true,
              showSymbol:false,
              stack:"Total",
              lineStyle:{
                width:0
              },
              emphasis:{
                focus:"series"
              },
              areaStyle:{
                opacity:.8,
                color:new $echarts.graphic.LinearGradient(0,0,0,1,[
                  {
                  offset:0,
                  color:"rgba(0,221,255)"
                  },
                  {
                  offset:1,
                  color:"rgba(77,119,255)"
                  },
              ])
              }
            },
            {
              name:"家电",
              type: "line",
              data: data.data.chartTwo.chartData.num.Electrical,
              smooth:true,
              showSymbol:false,
              stack:"Total",
              lineStyle:{
                width:0
              },
              emphasis:{
                focus:"series"
              },
              areaStyle:{
                opacity:.8,
                color:new $echarts.graphic.LinearGradient(0,0,0,1,[
                  {
                  offset:0,
                  color:"rgba(55,162,255)"
                  },
                  {
                  offset:1,
                  color:"rgba(116,21,219)"
                  },
              ])
              }
            },
            {
              name:"家居",
              type: "line",
              data: data.data.chartTwo.chartData.num.digit,
              smooth:true,
              showSymbol:false,
              stack:"Total",
              lineStyle:{
                width:0
              },
              emphasis:{
                focus:"series"
              },
              areaStyle:{
                opacity:.8,
                color:new $echarts.graphic.LinearGradient(0,0,0,1,[
                  {
                  offset:0,
                  color:"rgba(255,0,135)"
                  },
                  {
                  offset:1,
                  color:"rgba(135,0,157)"
                  },
              ])
              }
            },
            {
              name:"日化",
              type: "line",
              data: data.data.chartTwo.chartData.num.gear,
              smooth:true,
              showSymbol:false,
              stack:"Total",
              lineStyle:{
                width:0
              },
              emphasis:{
                focus:"series"
              },
              areaStyle:{
                opacity:.8,
                color:new $echarts.graphic.LinearGradient(0,0,0,1,[
                  {
                  offset:0,
                  color:"rgba(255,191,0)"
                  },
                  {
                  offset:1,
                  color:"rgba(224,62,76)"
                  },
              ])
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
  margin-bottom: .15rem;
}
</style>