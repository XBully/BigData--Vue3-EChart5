<template>
  <div>
    <header>
      <h1>ECharts+Vue3--大数据可视化</h1>
    </header>
    <!-- 大容器 -->
    <section class="container">
      <section class="itemLeft">
        <ItemPage>
          <ItemLeftTop/>
        </ItemPage>
        <ItemPage>
          <ItemLeftBottom/>
        </ItemPage>
      </section>
      <section class="itemCenter">
        <mapPage/>
      </section>
      <section class="itemRight">
        <ItemPage>
          <ItemRightTop/>
        </ItemPage>
        <ItemPage>
          <ItemRightBottom/>
        </ItemPage>
      </section>
    </section>
  </div>
</template>

<script>
import ItemPage from "@/components/itemPage.vue"

import ItemLeftTop from "@/components/itemLeftTop.vue"
import ItemLeftBottom from "@/components/itemLeftBottom.vue"
import ItemRightTop from "@/components/itemRightTop.vue"
import ItemRightBottom from "@/components/itemRightBottom.vue"
import mapPage from "@/components/itemMapPage.vue"

export default {
 components:{
  ItemPage,ItemLeftTop,ItemLeftBottom,ItemRightTop,ItemRightBottom,mapPage
 },


}
</script>

<style lang="less">
  header{
    height: 1rem;
    width: 100%;
    background-color: rgba(0,0,255,.2);
  }
  h1{
    font-style: 0.375rem;
    color: #fff;
    text-align: center;
    line-height: 1rem;
  }
  .container{
    min-width: 1200px;
    max-width: 1920px;
    margin: 0 auto;
    padding: .125rem .125rem 0;
    display: flex;
    .itemLeft,.itemRight{
      flex:3;
    }
    .itemCenter{
      flex:5;
      height: 10rem;
      border: 1px solid blue;
      padding: 0.125rem;
      margin: .25rem;
    }
  }
</style>