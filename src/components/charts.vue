<template>
  <div class="charts-lay">
    <p class="title">{{ chartData.title }}</p>
    <section ref="chart"></section>
  </div>
</template>

<script>
export default {
  name: "charts",
  components: {},
  props: ["chartData", "total"],

  data() {
    return {
      chartValueBgVal: 0,
    };
  },

  mounted() {
    console.log(this.chartData);

    this.chartValueBgVal = this.total - this.chartData.value;
    this.draw();
  },

  methods: {
    draw() {
      let container = this.$refs.chart;
      this.chart = this.$echarts.init(container);

      let option = {
        tooltip: {
          show: false,
          trigger: "item",
        },
        legend: {
          show: true,
          left: "30%",
          top: "center",
          icon: "circle",
          itemWidth: 8,
          itemHeight: 8,
          formatter: "占比"+this.chartData.persent + "%",
          data: [
            {
              name: this.chartData.title,
              itemStyle: {
                color: "rgb(255,159,127)",
              },
            },
          ],
          rich: {
            a: {
              color: "#6E7079",
              lineHeight: 22,
              align: "center",
            },
            hr: {
              borderColor: "#8C8D8E",
              width: "100%",
              borderWidth: 1,
              height: 0,
            },
            b: {
              color: "#4C5058",
              fontSize: 14,
              fontWeight: "bold",
              lineHeight: 33,
            },
            per: {
              color: "#fff",
              backgroundColor: "#4C5058",
              padding: [3, 4],
              borderRadius: 4,
            },
          },
        },

        series: [
          {
            name: "testChart",
            type: "pie",
            zlevel: "50",
            startAngle: "90",
            radius: ["60%", "80%"],
            center: ["15%", "50%"],

            avoidLabelOverlap: false,
            itemStyle: {
              borderRadius: 0,
              borderColor: "#fff",
              borderWidth: 0,
            },
            label: {
              show: false,
              position: "center",
            },
            labelLine: {
              show: false,
            },
            data: [
              {
                value: this.chartData.value,
                name: this.chartData.title,
                itemStyle: {
                  normal: {
                    color: "rgb(255,159,127)",
                  },
                },
                label: {
                  show: false,
                  fontSize: "20",
                  fontWeight: "bold",
                  position: "right",
                },
              },
              {
                //name:"bgCol",
                value: this.chartValueBgVal,
                //不需要显示的数据，颜色设置成和背景一样
                itemStyle: {
                  normal: {
                    color: "#d1d1d1",
                  },
                },
              },
            ],
          },
        ],
      };

      this.chart.setOption(option);
    },
  },
};
</script>

<style>
</style>
