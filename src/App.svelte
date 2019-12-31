<script>
  import { afterUpdate } from "svelte";
  import Highcharts from "highcharts";
  import highchartsMore from "highcharts-more";
  import funnel from "highcharts/modules/funnel";
  import data from "highcharts/modules/data";
  import exporting from "highcharts/modules/exporting";

  highchartsMore(Highcharts);
  data(Highcharts);
  exporting(Highcharts);
  funnel(Highcharts);

  let canvas;

  export let chartjson;
  export let highchartboxwidth;
  export let highchartboxheight;
  export let dataJSON;

  afterUpdate(() => {
    setTimeout(() => { 
        Highcharts.chart(canvas, chartjson); 
    }, 10);
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
    height: var(--chart-height, auto);
    width: var(--chart-width, auto);
  }
</style>

<div
  bind:this={canvas}
  style="--chart-height: {highchartboxheight}; --chart-width: {highchartboxwidth}">
  <slot />
</div>
<svelte:options tag="highchart-box" />
<!-- 
 For old Firefox enable these twofire 
  dom.webcomponents.enabled
  dom.webcomponents.customelements.enabled
This tells the Svelte compiler that this file is a custom element. 
We also have to include the "customElement: true" compiler setting in rollup configuration.
-->
