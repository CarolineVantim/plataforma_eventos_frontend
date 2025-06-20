<template>
  <div>
    <h3>Eventos com Vagas</h3>
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
          label: 'Total de Vagas Disponíveis por Tema',
          data: [],
          backgroundColor: 'rgba(255, 99, 132, 0.6)',
        }],
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            position: 'top',
          },
        },
        scales: {
          y: {
            beginAtZero: true
          }
        }
      }
    };
  },
  async mounted() {
    await this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get(`${process.env.VUE_APP_API_BASE_URL}/relatorios/eventos-com-vagas`);
        this.rawData = response.data;

        // Atualiza gráfico com os temas e a soma de vagas
        this.chartData.labels = this.rawData.map(item => item.tema);
        this.chartData.datasets[0].data = this.rawData.map(item => item.total_vagas_disponiveis);

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
