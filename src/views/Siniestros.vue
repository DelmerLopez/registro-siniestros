<template>
  <div class="siniestros">
    <h1>Siniestros</h1>
    <table>
      <thead>
        <tr>
          <th>Fecha Siniestro</th>
          <th>Fecha Reporte</th>
          <th>Placas</th>
          <th>Poliza</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="reporte in reportes" :key="reporte.id">
          <td>{{ reporte.fechaSiniestro }}</td>
          <td>{{ reporte.fechaReporte }}</td>
          <td>{{ reporte.vehiculo.placas }}</td>
          <td>{{ reporte.numeroPoliza }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      mensajeError: '',
      reportes: []
    }
  },
  methods: {
    recuperarReportesDanio() {
      axios.get('https://localhost:44382/api/ReporteDanio')
        .then(data => {
          this.reportes = data.data;
        }).catch(() => {
          this.mensajeError = "Ha ocurrido un error, intente más tarde";
        })
    }
  }, 
  beforeMount() {
    this.recuperarReportesDanio();
  },
}
</script>
