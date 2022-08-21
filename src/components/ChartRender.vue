<template>
  <h1>タイトル</h1>
  <Line
    :chart-data="chartData"
  />
</template>

<script>
import { Line } from 'vue-chartjs'
import 'chart.js/auto';

export default {
  name: 'ExampleChart',
  components: { Line },
  data() {
    return {
      chartData: {
        datasets: [
          {
            label: '睡眠時間(h)',
            backgroundColor: 'rgba(201, 0, 138, 0.5)',
            borderColor: 'rgba(201, 0, 138, 0.5)',
            data: {
              January: 10,
              February: 20,
              March: 40
            },
          },
          {
            label: '日中の眠気強度',
            backgroundColor: 'rgba(102, 153, 255, 1.0)',
            borderColor: 'rgba(102, 153, 255, 1.0)',
            data: {
              January: 15,
              April: 25,
              Jun: 35
            },
          },
          {
            label: '鼻詰まり強度',
            backgroundColor: 'rgba(102, 255, 102, 1.0)',
            borderColor: 'rgba(102, 255, 102, 1.0)',
            data: {
              July: 3,
              August: 12,
              September: 9
            },
          }
        ]
      }
    }
  }
}
</script>