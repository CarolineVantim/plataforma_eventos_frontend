<template>
  <b-container fluid>
    <b-row class="mb-4">

      <b-col cols="12" md="4">
        <EventosPorLocal />
      </b-col>
      <b-col cols="12" md="4">
        <EventosPorMes />
      </b-col>
      <b-col cols="12" md="4">
        <EventosPorPromotor />
      </b-col>
    </b-row>

    <b-row>

      <b-col cols="12" md="6">
        <EventosPorTema />
      </b-col>
      <b-col cols="12" md="6">
        <EventosPorVagas />
      </b-col>
    </b-row>
  </b-container>
</template>


<script>
import EventosPorLocal from '../components/graficos/EventosPorLocal.vue';
import EventosPorTema from '../components/graficos/EventosPorTema.vue';
import EventosPorMes from '../components/graficos/EventosPorMes.vue';
import EventosPorPromotor from '../components/graficos/EventosPorPromotor.vue';
import EventosPorVagas from '../components/graficos/EventosPorVagas.vue';

export default {
  name: 'GraficoView',
  components: {
    EventosPorLocal,
    EventosPorTema,
    EventosPorMes,
    EventosPorPromotor,
    EventosPorVagas,
  }
}
</script>

<style scoped>
.grafico-container {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  padding: 1rem;
}

.grafico-item {
  background: #f8f8f8;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 1px 4px rgba(0,0,0,0.1);
  min-height: 400px;
}
</style>
