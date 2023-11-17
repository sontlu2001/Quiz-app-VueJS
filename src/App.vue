<template>
  <v-app>
    <h1 color="primary">Primary Button</h1>
    <div id="chart">
      <v-flex  class="toolbar">
        <v-btn color="primary" id="one_month" @click="updateData('one_month')"
          :class="{ active: selection === 'one_month' }">
          1M
        </v-btn>

        <v-btn color="primary" id="six_months" @click="updateData('six_months')"
          :class="{ active: selection === 'six_months' }">
          6M
        </v-btn>

        <v-btn color="primary" id="one_year" @click="updateData('one_year')"
          :class="{ active: selection === 'one_year' }">
          1Y
        </v-btn>

        <v-btn color="primary" id="ytd" @click="updateData('ytd')" :class="{ active: selection === 'ytd' }">
          YTD
        </v-btn>

        <v-btn color="primary" id="all" @click="updateData('all')" :class="{ active: selection === 'all' }">
          ALL
        </v-btn>
      </v-flex>

      <div id="chart-timeline">
        <apexchart type="area" height="350" ref="chart" :options="chartOptions" :series="series"></apexchart>
      </div>
    </div>
  </v-app>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'
import Vue from 'vue'

Vue.use(VueApexCharts)
Vue.component('apexchart', VueApexCharts)

export default {
  data: function () {
    return {
      chartOptions: {
        chart: {
          id: 'vuechart-example'
        },
        xaxis: {
          type: 'datetime',
          labels: {
            format: 'dd/ MMM /yyyy',
            rotate: 45
          },
        },
        yaxis: {
          type: 'numeric',
          labels: {
            color: '#8e8d',
          }
        },
        dataLabels: {
          enabled: false
        },
        markers: {
          size: 5,
        },
        tooltip: {
          theme: 'dark',
          style: {
            background: '#333',
            color: '#fff',
          },
        },
        grid: {
          borderColor: '#e0e0e0',
          strokeDashArray: 4,
        },
      },
      series: [{
        name: 'people',
        data: [
          [1327359600000, 30.95],
          [1327446000000, 31.34],
          [1327532400000, 31.18],
          [1327618800000, 31.05],
          [1327878000000, 31.00],
          [1327964400000, 30.95],
          [1328050800000, 31.24],
          [1328137200000, 31.29],
          [1328223600000, 31.85],
          [1328482800000, 31.86],
          [1328569200000, 32.28],
          [1328655600000, 32.10],
          [1328742000000, 32.65],
          [1328828400000, 32.21],
          [1329087600000, 32.35],
          [1329174000000, 32.44],
          [1329260400000, 32.46],
          [1329346800000, 32.86],
          [1329433200000, 32.75],
          [1329778800000, 32.54],
          [1329865200000, 32.33],
        ]
      }],
      selection: 'one_month',
    }
  },
  methods: {
    updateData: function (timeline) {
      this.selection = timeline

      switch (timeline) {
        case 'one_month':
          this.$refs.chart.zoomX(
            new Date('28 Jan 2013').getTime(),
            new Date('27 Feb 2013').getTime()
          )
          break
        case 'six_months':
          this.$refs.chart.zoomX(
            new Date('27 Sep 2012').getTime(),
            new Date('27 Feb 2013').getTime()
          )
          break
        case 'one_year':
          this.$refs.chart.zoomX(
            new Date('27 Feb 2012').getTime(),
            new Date('27 Feb 2013').getTime()
          )
          break
        case 'ytd':
          this.$refs.chart.zoomX(
            new Date('01 Jan 2013').getTime(),
            new Date('27 Feb 2013').getTime()
          )
          break
        case 'all':
          this.$refs.chart.zoomX(
            new Date('23 Jan 2012').getTime(),
            new Date('27 Feb 2013').getTime()
          )
          break
        default:
      }
    }
  }
};
</script>

<style></style>


 
