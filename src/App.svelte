<script>
  import { afterUpdate } from "svelte";
  import Highcharts from "highcharts";
  import data from "highcharts/modules/data";
  let canvas;
  export let highchartstype;
  export let chartjson;
  data(Highcharts);
  afterUpdate(() => {
    setTimeout(() => {
      Highcharts.chart(canvas, chartjson);
    }, 0);
  });
</script>

<style>
  /* 
  Setting custom css variables enables the user to use css to target a custom
  element by an attribute and change css properties that you want to expose.
  */
  div {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 100%;
    width: 100%;
  }
</style>

<div role="chart" bind:this={canvas}>
  <slot />
</div>
<svelte:options tag="highchart-box" />
<!-- 

This tells the Svelte compiler that this file is a custom element. 
We also have to include the "customElement: true" compiler setting in rollup configuration.
-->
