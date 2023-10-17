<template>
<!-- 多轴横向可拖拽图 -->
  <div class="chart">
    <div id="lineChart" class="chartBox"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      lineOption: {
        tooltip: {
          trigger: "axis",
          // extraCssText: 'transform:rotate(-180deg)',
        },
        // 添加图例，若不显示，是series要添加name属性
        legend: {
          show: true,
          data: [
            { name: "平均降水量" },
            { name: "最大降水量" },
            { name: "最大积水量" },
          ],
          textStyle: { fontSize: 14, color: "#fff" },
          // 将图例显示到右侧
          // orient: "horizontal", // 垂直显示 vertical horizontal
          // y: "center", // 延Y轴居中
          // x: "left", // 居右显示
          // align: "left" // 颜色在左边
        },
        // 图距离右边的边距
        grid: {
          top: "70px",
          bottom: "40",
          left: "100",
          right: "50px",
        },
        xAxis: [
          {
            name: "  降\n  水\n  量\n(mm)",
            nameTextStyle: {
              // y轴单位的颜色
              color: "#fff",
              rotate: "90deg",
            },
            type: "value",
            // 刻度值颜色
            axisLabel: {
              textStyle: {
                color: "#fff",
              },
            },
            // y轴对应刻度背景先颜色
            splitLine: {
              lineStyle: {
                type: "dashed",
                color: "#878793",
              },
            },
          },
          {
            name: " 积\n 水\n 量\n(m)",
            nameTextStyle: {
              // y轴单位的颜色
              color: "#fff",
            },
            type: "value",
            // 刻度值颜色
            axisLabel: {
              textStyle: {
                color: "#fff",
              },
            },
            // y轴对应刻度背景先颜色
            splitLine: {
              lineStyle: {
                type: "dashed",
                color: "#878793",
              },
            },
          },
        ],
        yAxis: [
          {
            nameTextStyle: {
              // y轴单位的颜色
              color: "#fff",
            },
            // 刻度值颜色
            axisLabel: {
              textStyle: {
                color: "#fff",
              },
            },
            // y轴对应刻度背景先颜色
            splitLine: {
              show: false,
              lineStyle: {
                type: "dashed",
                color: "#878793",
              },
            },
            type: "category",
            data: [
              "07/29 09:00",
              "07/29 09:00",
              "07/29 09:00",
              "07/29 09:00",
              "07/29 09:00",
              "07/29 09:00",
              "07/29 09:00",
              "07/29 09:00",
            ],
          },
        ],
        series: [
          {
            animation: false, //转换成docx文档要设置成false
            name: "平均降水量",
            data: [10, 20, 30, 10, 20, 30, 10, 20, 30, 10, 20, 30],
            type: "line",
            xAxisIndex: 0,
            itemStyle: {
              color: "#6A9BF6",
            },
          },
          {
            name: "最大降水量",
            data: [10, 20, 30],
            type: "line",
            // 坐标轴右侧添加刻度
            xAxisIndex: 0,
            itemStyle: {
              color: "#7AD55F",
            },
          },
          {
            name: "最大积水量",
            data: [10, 20, 30],
            type: "line",
            // 坐标轴右侧添加刻度
            xAxisIndex: 1,
            itemStyle: {
              color: "#FC982A",
            },
          },
        ],
        dataZoom: [
          {
            type: "slider",
            orient: "vertical",
            yAxisIndex: 0,
            start: 100,
            end: 40,
            left: 10,
            width: 15,
          },
        ],
      },
    };
  },
  mounted() {
    const res = {
      lineXais: [
        "07/04/15",
        "07/04/14",
        "07/04/13",
        "07/04/12",
        "07/04/11",
        "07/04/10",
        "07/04/09",
        "07/04/08",
        "07/04/07",
        "07/04/06",
        "07/04/05",
      ],
      maxAccWater: [
        0, 0.017411852, 0.0775616, 0.1704156, 0.28631964, 0.40197968,
        0.48072654, 0.4458102, 0.2885743, 0.19492057, 0.049606666,
      ],
      maxPrcp: [
        0, 0.30517578, 2.4414062, 3.0517578, 5.7978516, 28.685059, 34.330566,
        51.419434, 85.59717, 60.269043, 53.555664,
      ],
      meanPrcp: [
        0, 0.0035226445, 0.15887742, 0.38840562, 1.7671837, 7.10754, 9.332118,
        9.037015, 11.376251, 10.539332, 8.68557,
      ],
    };
    // 设置间隔
    this.lineOption.xAxis[1].min = Math.floor(Math.min(...res.maxAccWater));
    this.lineOption.xAxis[1].max = Math.ceil(Math.max(...res.maxAccWater));
    this.lineOption.xAxis[0].min = Math.floor(
      Math.min(...res.meanPrcp, ...res.maxPrcp)
    );
    this.lineOption.xAxis[0].max = Math.ceil(
      Math.max(...res.meanPrcp, ...res.maxPrcp)
    );
    this.lineOption.xAxis[0].interval =
      (this.lineOption.xAxis[0].max - this.lineOption.xAxis[0].min) / 5;
    this.lineOption.xAxis[1].interval =
      (this.lineOption.xAxis[1].max - this.lineOption.xAxis[1].min) / 5;

    this.lineOption.yAxis[0].data = res.lineXais;
    this.lineOption.series[0].data = res.meanPrcp;
    this.lineOption.series[1].data = res.maxPrcp;
    this.lineOption.series[2].data = res.maxAccWater;
    const chartLine = document.getElementById("lineChart");
    const myChartLine = this.echarts.init(chartLine);
    myChartLine.setOption(this.lineOption);
  },
};
</script>
<style lang="scss" scoped>
#lineChart {
  width: 100%;
  height: 450px;
}
</style>