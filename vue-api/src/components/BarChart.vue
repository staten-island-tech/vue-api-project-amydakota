<template>
    <div class="container">
        <Bar v-if="loaded" :data="chartData" />
    </div>
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
import {ref, onMounted} from 'vue'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
  data: () => ({
    loaded: false,
    chartData: null
  }),
  async onMounted () {
    this.loaded = false

    try {
      const { userlist } = await fetch('https://data.cityofnewyork.us/resource/h9gi-nx95.json')
      this.chartdata = userlist

      this.loaded = true
      
    } catch (e) {
      console.error(e)
    }
  }
}

</script>

<style scoped>

</style>