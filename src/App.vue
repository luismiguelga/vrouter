<template>
  <div class="body">
    <div class="tabla">
      <h1>Tabla</h1>
      <table>
        <thead>
          <tr>
            <th>Vehiculo</th>
            <th>Numasientos</th>
            <th>Horarios</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(dato, index) in guardardatos" :key="index">
            <td>{{ dato.numero_asiento }}</td>
            <td>{{ dato.vehiculo }}</td>
            <td>{{ dato.horario }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
  

<script setup>
import { ref } from 'vue';
import { onMounted } from 'vue';
import axios from 'axios';

let guardardatos = ref([])

async function ObtenerDatos() {
  const response = await axios.get(`https://transporte-0ydp.onrender.com/api/transporte/transbusca`);
  const data= response.data
  data.transporte.forEach((transporte) => {
    guardardatos.value.push({
      numero_asiento: transporte.NumAsientos,
      vehiculo: transporte.Vehiculo,
      horario: transporte.horario
    });
  })



  console.log(response.data);
}

onMounted(() => {
  ObtenerDatos()
})


</script>


<style scoped>
.body {
  display: flex;






  flex-direction: column;
  align-items: center;
  text-align: center;
  height: 100vh;
  background-color: #a3ffff;
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: rgba(0, 0, 0, 0.87);
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;
}

.modal-body {
  display: flex;
  flex-direction: column;
  gap: 25px;
  background-color: rgb(80, 80, 80);
  color: white;
}

.tabla {
  border-radius: 10px;
  border: 5px solid black;
  padding: 20px;
  background-color: rgb(255, 255, 255);
}

#bt {
  color: rgb(255, 255, 255);
  font-weight: bolder;
  font-size: 17px;
}

table {
  border-collapse: collapse;
  font-size: 20px;
  text-align: center;
  width: 1300px;
}

th,
td {
  border: 3px solid rgb(0, 0, 0);
  padding: 5px;

}

th {
  background-color: rgb(244, 240, 14);
}

button {
  margin: 5px;
}

#BT {
  background-color: rgb(14, 182, 45);
  border-radius: 20px;
  font-size: 25px;
  font-weight: bolder;
  padding: 10px;
}

.h {
  background-color: rgb(80, 78, 78);
  border: 3px solid black;
}

#eliminar {
  background-color: orange;
}

#editar {
  background-color: cornflowerblue;
}

.error-message {
  color: red;
}
</style>