<template>
  <h1>睡眠・体調データ</h1>
  <input type="file" @change="importCsv" />
  <Line
    :chart-data="chartData"
    :height="height"
    :width="width"
  />
</template>

<script>
import { Line } from 'vue-chartjs'
import 'chart.js/auto';

export default {
  name: 'ExampleChart',
  components: { Line },
  methods: {
    importCsv: function (e) {
      const importFile = e.target.files[0];
      const reader = new FileReader();
      let timeOfSleepingData = {};
      let intensityOfSleepinessData = {};
      let intensityOfNasalCongestion = {};
      reader.readAsText(importFile);
      reader.onload = () => {
        let lines = reader.result.split('\r\n');
        for (const string of lines) {
          var dataElement = string.split(',');
          timeOfSleepingData[dataElement[0]] = dataElement[1];
          intensityOfSleepinessData[dataElement[0]] = dataElement[2];
          intensityOfNasalCongestion[dataElement[0]] = dataElement[3];
        }
        this.chartData.datasets[0].data = timeOfSleepingData;
        this.chartData.datasets[1].data = intensityOfSleepinessData;
        this.chartData.datasets[2].data = intensityOfNasalCongestion;
      };
    }
  },
  data() {
    return {
      chartData: {
        datasets: [
          {
            label: '睡眠時間(h)',
            backgroundColor: 'rgba(201, 0, 138, 0.5)',
            borderColor: 'rgba(201, 0, 138, 0.5)',
            data: {
              January: 100,
              February: 200,
              March: 400
            }
          },
          {
            label: '日中の眠気強度(0〜4)',
            backgroundColor: 'rgba(102, 153, 255, 1.0)',
            borderColor: 'rgba(102, 153, 255, 1.0)',
            data: {
              January: 15,
              April: 25,
              Jun: 35
            },
          },
          {
            label: '鼻詰まり強度(0〜4)',
            backgroundColor: 'rgba(102, 255, 102, 1.0)',
            borderColor: 'rgba(102, 255, 102, 1.0)',
            data: {
              July: 3,
              August: 12,
              September: 9
            },
          }
        ]
      },
      height: window.innerHeight / 2,
      width: window.innerWidth,
    }
  }
}
</script>