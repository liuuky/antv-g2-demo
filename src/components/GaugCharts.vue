<template>
  <div id="myChart" ref="myCharts"></div>
</template>

<script lang="ts">
import { defineComponent, nextTick, onMounted, ref } from "vue";
import * as echarts from "echarts";

export default defineComponent({
  name: "GaugCharts",
  setup() {
    const myCharts = ref(null);

    const option = {
      backgroundColor: "black",
      title: {
        x: "center",
        y: "63%",
        bottom: 50,
        text: "运营状况",
        subtext: "General operation",
        textStyle: {
          fontWeight: "bold",
          fontSize: 35,
          color: "#0095ff",
        },
        subtextStyle: {
          fontWeight: "normal",
          fontSize: 20,
          color: "#0095ff",
        },
      },
      tooltip: {
        format: (params) => {
          console.log(params);
        },
      },
      graphic: {
        elements: [
          {
            type: "image",
            style: {
              // image: "./center.png",
              width: 190,
              height: 190,
            },
            left: "center",
            top: "center",
          },
        ],
      },
      series: [
        {
          splitNumber: 13, //刻度数量
          radius: "66%", //图表尺寸
          axisLine: {
            show: false,
            lineStyle: {
              width: 10,
              shadowBlur: 0,
              color: [[1, "black"]],
            },
          },
          splitLine: {
            distance: -10,
            length: 10,
            lineStyle: {
              color: "#0095ff",
            },
          },
        },
        {
          radius: "62%",
          splitNumber: "52",
          axisLine: {
            lineStyle: {
              color: [[1, "#0095ff"]],
              width: 10,
            },
          },
          splitLine: {
            distance: -10,
            length: 10,
            lineStyle: {
              color: "black",
              width: 4,
            },
          },
        },
        {
          radius: "56%",
          splitNumber: 0,
          axisLine: {
            // 坐标轴线
            lineStyle: {
              color: [[1, "#0095ff"]], // 属性lineStyle控制线条样式
              width: 2,
            },
          },
          splitLine: {
            // 分隔线
            show: false,
          },
        },
        {
          splitNumber: "22",
          radius: "52%",
          axisLine: {
            lineStyle: {
              color: [
                [0, "#ff0090"],
                [1, "#631643"],
              ],
              width: 25,
            },
          },
          splitLine: {
            distance: -25,
            length: 25,
            lineStyle: {
              color: "black",
              width: 8,
            },
          },
        },
        {
          radius: "42%",
          splitNumber: 0,
          axisLine: {
            // 坐标轴线
            lineStyle: {
              color: [[1, "#0095ff"]], // 属性lineStyle控制线条样式
              width: 2,
            },
          },
          splitLine: {
            show: false,
          },
        },
        {
          radius: "38%",
          splitNumber: "22",
          axisLine: {
            lineStyle: {
              color: [
                [0, "#fcff00"],
                [1, "#626317"],
              ],
              width: 20,
            },
          },
          splitLine: {
            distance: -20,
            length: 20,
            lineStyle: {
              color: "black",
              width: 6,
            },
          },
        },
      ],
    };

    const initCharts = () => {
      for (let i = 0; i < option.series.length; i++) {
        option.series[i].type = "gauge";
        option.series[i].startAngle = 220;
        option.series[i].endAngle = -40;
        option.series[i].center = ["50%", "50%"];
        option.series[i].axisTick = { show: false };
        option.series[i].axisLabel = { show: false };
        option.series[i].pointer = { show: false };
        option.series[i].detail = { show: false };
      }

      // const myChart = echarts.init(document.getElementById("myChart")); //get()方法作用：将jQuery对象转Dom对象
      console.log("myCharts.value", myCharts.value);
      const myChart = echarts.init(myCharts.value); //get()方法作用：将jQuery对象转Dom对象
      myChart.setOption(option);

      let num1 = 0,
        num2 = 0;
      let myInterval = setInterval(function () {
        num1 += Math.round(Math.random()) === 0 ? 0.011 : 0.005;
        num2 += Math.round(Math.random()) === 0 ? 0.011 : 0.005;
        if (num1 >= 1) num1 = 0;
        if (num2 >= 1) num2 = 0;
        option.series[3].axisLine.lineStyle.color = [
          [num1, "#ff0090"],
          [1, "#631643"],
        ];
        option.series[5].axisLine.lineStyle.color = [
          [num2, "#fcff00"],
          [1, "#626317"],
        ];
        myChart.setOption(option);
      }, 50);
    };

    onMounted(() => {
      nextTick(() => {
        initCharts();
      });
    });

    return {
      option,
      myCharts,
    };
  },
});
</script>

<style scoped>
html,
body {
  width: 100%;
  height: 100%;
}

#myChart {
  width: 80%;
  height: 70%;
  position: fixed;
  top: 15%;
  left: 10%;
}
</style>
