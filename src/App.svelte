<script>
  import { afterUpdate } from "svelte";
  import Highcharts from "highcharts";
  import data from "highcharts/modules/data";
  export let highchartstype;
  export let containerid;
  data(Highcharts);
  afterUpdate(() => {
    setTimeout(() => {
      Highcharts.chart(containerid, {
        title: {
          text: "Global temperature change"
        },

        subtitle: {
          text: "Data input from CSV"
        },

        data: {
          csvURL: "https://demo-live-data.highcharts.com/vs-load.csv",
          enablePolling: true,
          dataRefreshRate: 1
        },

        plotOptions: {
          series: {
            marker: {
              enabled: false
            }
          }
        },

        series: [
          {
            type: highchartstype,
            color: "#c4392d",
            negativeColor: "#5679c4",
            fillOpacity: 0.5
          }
        ]
      });
    }, 0);
  });
</script>

<!-- 
This tells the Svelte compiler that this file is a custom element. 
We also have to include the "customElement: true" compiler setting in rollup configuration.
-->
<svelte:options tag="highchart-box" />
