<template>
  <div>
    <h3>Eventos por Promotor</h3>
    <BaseChart
      type="bar"
      :data="chartData"
      :options="chartOptions"
    />
  </div>
</template>

<script>
import BaseChart from './BaseChart.vue';
import axios from 'axios';

export default {
  components: { BaseChart },
  data() {
    return {
      rawData: [],
      chartData: {
        labels: [],
        datasets: [{
          label: 'Eventos por Promotor',
          data: [],
          backgroundColor: 'rgba(75, 192, 192, 0.5)',
        }],
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
      }
    };
  },
  async mounted() {
    await this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get(`${process.env.VUE_APP_API_BASE_URL}/relatorios/eventos-por-promotor`);
        this.rawData = response.data;

        this.chartData.labels = this.rawData.map(item => item.promotor);
        this.chartData.datasets[0].data = this.rawData.map(item => item.quantidade);

      } catch (error) {
        console.error('Erro ao buscar dados', error);
      }
    },
  }
}
</script>

<style scoped>
.grafico-box {
  height: 150px;
  width: 50%;
  position: relative;
}
</style>
