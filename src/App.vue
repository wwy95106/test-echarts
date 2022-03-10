<template>
  <div id="app">

    <div class="container">

      <div class="total-number-lay">
        <p class="title">上线设备总量(台)</p>
        <section>
          <span class="value total-value">{{totalNumber}}</span>
        </section>
      </div>

      <div class="charts-view-lay">
        <echartsView
        v-for="(items, index) in chartsD"
        :key="index"
        v-bind:chartData="items"
        v-bind:total="totalNumber"
      />
      </div>
    </div>

  </div>
</template>

<script>
import echartsView from "./components/charts.vue";

export default {
  name: "App",
  components: {
    echartsView,
  },

  
  data() {
    return {
      totalNumber:0,
      chartsD: [
        {
          title: "世昕",
          persent: 67.13,
          value: 143,
        },
        {
          title: "航天能源",
          persent: 67.13,
          value: 34,
        },
        {
          title: "科尼",
          persent: 67.13,
          value: 41,
        },
        {
          title: "测试1",
          persent: 67.13,
          value: 52,
        },
        {
          title: "测试2",
          persent: 67.13,
          value: 23,
        },
        {
          title: "测试3",
          persent: 67.13,
          value: 18,
        },
      ],
    };
  },
  created(){
    
    this.totalNumber = this.initTotal();
  },
  methods:{
    initTotal(){
      let total = 0;
      for(let index in this.chartsD){
        total += this.chartsD[index].value;
      }
      return total;
    }
  }
};
</script>

<style>
* {
  padding:0;
  margin:0;
  box-sizing:border-box;
}
html,body {
  background:#f1f1f1;
  padding:12px;
}
#app {
  width:100%;
  height:auto;
}

.container {
  width:100%;
  height:160px;
  
  display: flex;
  justify-content:flex-start;
  flex-wrap:nowrap;
  align-items:center;

  background-color:#fff;
  box-shadow: 0px 0px 5px #d1d1d1;
  padding:24px 12px;
}

.total-number-lay {
  width:200px;
  height:100%;
}

.charts-view-lay {
  width:calc(100% - 200px);
  height:100%;
}

.total-number-lay .title,
.charts-view-lay .title {
  height:40px;
  line-height:40px;
  color:#555;
  font-size:14px;
  font-weight:bold;
}

.total-number-lay section,
.charts-view-lay section {
  height:calc(100% - 40px);
}

.charts-view-lay {
  display: flex;
  justify-content:flex-start;
  flex-wrap:nowrap;
  align-items:center;
}

.charts-lay {
  width:33.3333%;
  height:100%;
  padding-left:12px;
  border-left:1px solid #c1c1c1;
}

.total-value {
  font-size:30px;
  font-weight:bold;
  font-family: "黑体";
  color:#333;
}

</style>
