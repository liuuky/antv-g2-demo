<template>
  <div id="container" ref="containerRef"></div>
</template>

<script lang="ts">
import {
  defineComponent,
  nextTick,
  onMounted,
  onUnmounted,
  PropType,
  reactive,
  ref,
  shallowRef,
  watchEffect,
} from "vue";
import { Chart } from "@antv/g2";

export interface DataPorps {
  year: string;
  sales: number;
}

export default defineComponent({
  name: "ChartTest",
  props: {
    data: {
      // type: Array as PropType<any[]>,
      type: Array as PropType<DataPorps[]>,
      require: true,
      default: () => [],
    },
  },
  setup(props, ctx) {
    console.log("props", props);
    console.log("ctx", ctx);

    const containerRef = ref();

    const bar = shallowRef<Chart | null>(null);
    // const bar = ref<Chart | null>(null);

    const initChart = () => {
      const chart = new Chart({
        container: "container",
        autoFit: true,
        width: 400,
        height: 300,
      });

      // chart.data(data);
      chart.data(props.data);

      chart.scale("sales", {
        alias: "销量",
        min: 0,
        max: 200,
        type: "linear",
        tickCount: 10,
        // nice: true
      });

      chart.axis("sales", {
        title: {},
      });

      chart.line().position("year*sales").color("type");
      // chart.area().adjust('stack').position("year*sales").color('type');
      chart
        .area()
        // .adjust("dodge")
        .position("year*sales")
        .tooltip(false)
        .color("type", [
          "l(100) 0:#206EF7FF 1:#206EF700",
          "l(100) 0:#29C9EAFF 1:#29C9EA00",
          "l(100) 0:#722ED1FF 1:#722ED100",
          "l(100) 0:#FF4383FF 1:#FF438300",
          "l(100) 0:#FFBF00FF 1:#FFBF0000",
        ]);

      // chart.line().adjust('stack').position("year*sales").color('#5AD8A6');
      // chart.area().adjust('stack').position("year*sales").color('l(270) 0:#007BC7 0.5:#EE0000');

      // chart.line().adjust("stack").position("year*sales").color("type").shape('smooth');
      // // chart.area().adjust('stack').position("year*sales").color('type');
      // chart
      //   .area()
      //   .adjust("stack")
      //   .position("year*sales")
      //   .tooltip(false)
      //   .color("type", [
      //     "l(100) 0:#206EF7FF 1:#206EF700",
      //     "l(100) 0:#29C9EAFF 1:#29C9EA00",
      //     "l(100) 0:#722ED1FF 1:#722ED100",
      //     "l(100) 0:#FF4383FF 1:#FF438300",
      //     "l(100) 0:#FFBF00FF 1:#FFBF0000",
      //   ])
      //   .shape('smooth');

      chart
        .interval()
        // .adjust('stack')
        .position("year*sales")
        // .color('year', ['l(270) 0:#007BC7 1:#00DFFD'])
        .color('type')
        .size(11);
        // .color({
        //   fields: ["year"],
        //   // fields: ["sales"],
        //   values: ["#1890ff", "#5AD8A6"],
        // });
      // .color('#5AD8A6');
      // .color('sales', '#BAE7FF-#1890FF-#0050B3');

      chart.tooltip({
        showMarkers: false,
        // showMarkers: true,
        shared: true,
      });

      // chart.legend(false);

      chart.interaction("active-region"); // 使用 active-region 交互行为

      // chart.interval().color({
      //   fields: ["x"],
      //   values: ["#1890ff", "#5AD8A6"],
      // });

      chart.render();

      bar.value = chart;
    };

    const changeData = () => {
      console.log("changeData");
      if (bar.value) {
        // bar.value.changeData(data);
        bar.value.changeData(props.data);
      }
      bar.value?.render();
    };

    const resizeChart = () => {
      if (bar.value) {
        bar.value?.forceFit();
      }
      console.log("resizeChart");
    };

    const destory = () => {
      if (bar.value) {
        bar.value?.destroy();
        bar.value = null;
      }
    };

    onMounted(() => {
      console.log("containerRef", containerRef.value);
      nextTick(() => {
        initChart();
      });
      // initChart();
      window.addEventListener("resize", resizeChart, false);

      // setTimeout(() => {
      //   props.data[0].sales = 200;
      //   console.log(props.data);
      // }, 3000);
    });

    watchEffect(() => {
      changeData();
      console.log("watchEffect-changeData");
    });

    onUnmounted(() => {
      destory();
      console.log("destory");
    });

    return {
      containerRef,
    };
  },
});
</script>

<style></style>
