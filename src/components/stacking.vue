<template>
<!-- 堆叠图 -->
  <div class="stacking">
    <div id="stackingChart" class="chartBox"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      dataServiceObjChange: {
        legend: {
          data: [
            "部机关司局",
            "部系统单位",
            "其他部委",
            "省级单位",
            "规划院内部",
            "高校和科研机构",
            "社会公众",
          ],
          left: "20%",
          bottom: 0,
          textStyle: {
            fontSize: 10,
            color:'#fff'
          },
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "shadow",
          },
        },
        xAxis: {
          data: ['10/1','10/2','10/3','10/4','10/5'],
          name: "",
        //   axisLine: { onZero: true },
          splitLine: { show: false },
          splitArea: { show: false },
          axisTick: {
            // 坐标轴刻度相关配置
            show: false, // 是否显示坐标轴刻度
          },
          axisLabel: {
            // 坐标轴刻度标签相关配置
            fontSize: 10,
          },
          axisLine: {
            // 坐标轴轴线相关配置
            show: false, // 是否显示坐标轴轴线
          },
        },
        yAxis: {
          axisTick: {
            // 坐标轴刻度相关配置
            show: false, // 是否显示坐标轴刻度
          },
          axisLabel: {
            // 坐标轴刻度标签相关配置
            fontSize: 10,
          },
          axisLine: {
            // 坐标轴轴线相关配置
            show: false, // 是否显示坐标轴轴线
          },
        },
        grid: {
          bottom: 100,
        },
        series: [
          {
            barMaxWidth: 40,
            animation: false,
            name: "部机关司局",
            type: "bar",
            stack: "one", //堆叠的关键属性
            color: "#ff0000",
            label: {
              show: true,
              position: "inside",
              color: "#fff",
              fontSize: 10,
            },
            data: [10,20,30,40,50],
          },
          {
            barMaxWidth: 40,
            animation: false,
            name: "部系统单位",
            type: "bar",
            stack: "one",
            color: "#ffc000",
            label: {
              show: true,
              position: "inside",
              color: "#fff",
              fontSize: 10,
            },
            data: [10,20,30,40,50],
          },
          {
            barMaxWidth: 40,
            animation: false,
            name: "其他部委",
            type: "bar",
            stack: "one",
            color: "#ffff00",
            label: {
              show: true,
              position: "inside",
              color: "#fff",
              fontSize: 10,
            },
            data: [10,20,30,40,50],
          },
          {
            barMaxWidth: 40,
            animation: false,
            name: "省级单位",
            type: "bar",
            stack: "one",
            color: "#92d050",
            label: {
              show: true,
              position: "inside",
              color: "#fff",
              fontSize: 10,
            },
            data: [10,20,30,40,50],
          },
          {
            barMaxWidth: 40,
            animation: false,
            name: "规划院内部",
            type: "bar",
            stack: "one",
            color: "#00b0f0",
            label: {
              show: true,
              position: "inside",
              color: "#fff",
              fontSize: 10,
            },
            data: [10,20,30,40,50],
          },
          {
            barMaxWidth: 40,
            animation: false,
            name: "高校和科研机构",
            type: "bar",
            stack: "one",
            color: "#00b050",
            label: {
              show: true,
              position: "inside",
              color: "#fff",
              fontSize: 10,
            },
            data: [10,20,30,40,50],
          },
          {
            barMaxWidth: 40,
            animation: false,
            name: "社会公众",
            type: "bar",
            stack: "one",
            color: "#7030a0",
            label: {
              show: true,
              position: "inside",
              color: "#fff",
              fontSize: 10,
            },
            data: [10,20,30,40,50],
          },
        ],
      },
    };
  },
  mounted() {
    const chartLine = document.getElementById("stackingChart");
    const myChartLine = this.echarts.init(chartLine);
    myChartLine.setOption(this.dataServiceObjChange);
  },
};
</script>
<style lang="scss" scoped>
#stackingChart {
  width: 100%;
  height: 450px;
}</style>
