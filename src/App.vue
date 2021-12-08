<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// import HelloWorld from "./components/HelloWorld.vue";

import ChartTest from "./components/ChartTest.vue";
import GaugCharts from "./components/GaugCharts.vue";
import GaugCharts2 from "./components/GaugCharts2.vue";
import GaugCharts3 from "./components/GaugCharts3.vue";
import { reactive } from "vue";

const data = reactive([
  { year: "1951 年", sales: 98, type: 'Asia' },
  { year: "1952 年", sales: 52, type: 'Asia' },
  { year: "1956 年", sales: 61, type: 'Asia' },
  { year: "1957 年", sales: 145, type: 'Asia' },
  { year: "1958 年", sales: 48, type: 'Asia' },
  { year: "1959 年", sales: 38, type: 'Asia' },
  { year: "1960 年", sales: 38, type: 'Asia' },
  { year: "1962 年", sales: 38, type: 'Asia' },

  { year: "1951 年", sales: 48, type: 'Oceania' },
  { year: "1952 年", sales: 82, type: 'Oceania' },
  { year: "1956 年", sales: 61, type: 'Oceania' },
  { year: "1957 年", sales: 95, type: 'Oceania' },
  { year: "1958 年", sales: 48, type: 'Oceania' },
  { year: "1959 年", sales: 118, type: 'Oceania' },
  { year: "1960 年", sales: 38, type: 'Oceania' },
  { year: "1962 年", sales: 18, type: 'Oceania' },
]);

// const data = reactive([
//   { year: "1951 年", sales: 1, type: 'Asia' },
//   { year: "1952 年", sales: 1, type: 'Asia' },
//   { year: "1956 年", sales: 1, type: 'Asia' },
//   { year: "1957 年", sales: 1, type: 'Asia' },
//   { year: "1958 年", sales: 1, type: 'Asia' },
//   { year: "1959 年", sales: 1, type: 'Asia' },
//   { year: "1960 年", sales: 1, type: 'Asia' },
//   { year: "1962 年", sales: 1, type: 'Asia' },
// ]);
</script>

<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <!-- <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" /> -->
  <ChartTest :data="data" />
  <br />
  <GaugCharts />
  <br />
  <GaugCharts2 />
  <br />
  <GaugCharts3 />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
