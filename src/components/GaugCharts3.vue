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
        // text: "运营状况",
        // subtext: "General operation",
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
        // {
        //   splitNumber: 13, //刻度数量
        //   radius: "66%", //图表尺寸
        //   axisLine: {
        //     show: false,
        //     lineStyle: {
        //       width: 10,
        //       shadowBlur: 0,
        //       color: [[1, "black"]],
        //     },
        //   },
        //   splitLine: {
        //     distance: -10,
        //     length: 10,
        //     lineStyle: {
        //       color: "#0095ff",
        //     },
        //   },
        // },
        // {
        //   radius: "62%",
        //   splitNumber: "52",
        //   axisLine: {
        //     lineStyle: {
        //       color: [[1, "#0095ff"]],
        //       width: 10,
        //     },
        //   },
        //   splitLine: {
        //     distance: -10,
        //     length: 10,
        //     lineStyle: {
        //       color: "black",
        //       width: 4,
        //     },
        //   },
        // },
        // {
        //   radius: "56%",
        //   splitNumber: 0,
        //   axisLine: {
        //     // 坐标轴线
        //     lineStyle: {
        //       color: [[1, "#0095ff"]], // 属性lineStyle控制线条样式
        //       width: 2,
        //     },
        //   },
        //   splitLine: {
        //     // 分隔线
        //     show: false,
        //   },
        // },
        // {
        //   splitNumber: "22",
        //   radius: "52%",
        //   axisLine: {
        //     lineStyle: {
        //       color: [
        //         [0, "#ff0090"],
        //         [1, "#631643"],
        //       ],
        //       width: 25,
        //     },
        //   },
        //   splitLine: {
        //     distance: -25,
        //     length: 25,
        //     lineStyle: {
        //       color: "black",
        //       width: 8,
        //     },
        //   },
        // },
        // {
        //   radius: "42%",
        //   splitNumber: 0,
        //   axisLine: {
        //     // 坐标轴线
        //     lineStyle: {
        //       color: [[1, "#0095ff"]], // 属性lineStyle控制线条样式
        //       width: 2,
        //     },
        //   },
        //   splitLine: {
        //     show: false,
        //   },
        // },
        {
          radius: "100%",
          splitNumber: "22",
          axisLine: {
            lineStyle: {
              color: [
                // [0, "#fcff00"],
                // [1, "#626317"],
                [0, "#1c8ee6"],
                [1, "#052e64"],
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
          data: [
            {
              value: 0,
            },
          ],
          progress: {
            show: true,
            width: 20,
          },
          detail: {
            valueAnimation: true,
            width: "60%",
            lineHeight: 40,
            borderRadius: 8,
            // offsetCenter: [0, "-15%"],
            offsetCenter: [0, "-5%"],
            // fontSize: 60,
            fontSize: 34,
            fontWeight: "bolder",
            formatter: "{value}%",
            // color: "auto",
            color: "#fff",
          },
          itemStyle: {
            color: {
              type: "linear",
              x: 0,
              y: 1,
              x2: 1,
              y2: 0,
              global: false,
              colorStops: [
                {
                  offset: 0,
                  color: "#1c8ee6", // 0% 处的颜色
                },
                {
                  offset: 1,
                  color: "#36d0f6", // 100% 处的颜色
                },
              ],
            },
          },
        },
        {
          radius: "68%",
          splitNumber: 0,
          axisLine: {
            // 坐标轴线
            lineStyle: {
              color: [[1, "#1c8ee6"]], // 属性lineStyle控制线条样式
              width: 2
            },
          },
          splitLine: {
            show: false,
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
        // option.series[i].detail = { show: false };
      }

      // const myChart = echarts.init(document.getElementById("myChart")); //get()方法作用：将jQuery对象转Dom对象
      console.log("myCharts.value", myCharts.value);
      const myChart = echarts.init(myCharts.value); //get()方法作用：将jQuery对象转Dom对象
      myChart.setOption(option);

      let num1 = 0,
        num2 = 0;
      let myInterval = setInterval(function () {
        // num1 += Math.round(Math.random()) === 0 ? 0.011 : 0.005;
        // num2 += Math.round(Math.random()) === 0 ? 0.011 : 0.005;
        // if (num1 >= 1) num1 = 0;
        // if (num2 >= 1) num2 = 0;
        // option.series[3].axisLine.lineStyle.color = [
        //   [num1, "#ff0090"],
        //   [1, "#631643"],
        // ];
        // option.series[5].axisLine.lineStyle.color = [
        //   [num2, "#fcff00"],
        //   [1, "#626317"],
        // ];

        // num2 += (Math.random()).toFixed(2);
        // num2 += Math.round(Math.random()) === 0 ? 0.011 : 0.005;
        // num2 += (Math.random()).toFixed(2) === 0 ? 0.011 : 0.005;
        num2 += Number(Math.random().toFixed(2));
        if (num2 >= 1) num2 = 0;

        console.log(num2);

        option.series[0].axisLine.lineStyle.color = [
          // [num2, "#fcff00"],
          // [1, "#626317"],
          [num2, "#1c8ee6"],
          [1, "#052e64"],
        ];

        // option.series[0].axisLine.lineStyle.color = [
        //   [
        //     num2,
        //     {
        //       type: "linear",
        //       x: 0,
        //       y: 1,
        //       x2: 1,
        //       y2: 0,
        //       global: false,
        //       colorStops: [
        //         {
        //           offset: 0,
        //           color: "#1c8ee6", // 0% 处的颜色
        //         },
        //         {
        //           offset: 1,
        //           color: "#36d0f6", // 100% 处的颜色
        //         },
        //       ],
        //     },
        //   ],
        //   [1, "#052e64"],
        // ];
        // option.series[0].data[0].value = num2.toFixed(2) * 100;
        option.series[0].data[0].value = Math.round(num2 * 100);
        myChart.setOption(option);
      }, 1000);
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

/* #myChart {
  width: 80%;
  height: 70%;
  position: fixed;
  top: 15%;
  left: 10%;
} */

#myChart {
  width: 200px;
  height: 200px;
  position: fixed;
  top: 15%;
  left: 10%;
}
</style>
