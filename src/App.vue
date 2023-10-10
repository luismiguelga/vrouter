<template>
  <div class="body">
    <div class="tabla">
      <q-table
        title="Tabla"
        :rows="guardardatos"
        :columns="columns"
        row-key="numero_asiento"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const guardardatos = ref([]);
const columns = [
  {
    name: 'vehiculo',
    required: true,
    label: 'Vehiculo',
    align: 'left',
    field: 'vehiculo',
    sortable: true
  },
  {
    name: 'numero_asiento',
    label: 'Numasientos',
    field: 'numero_asiento',
    sortable: true
  },
  {
    name: 'horario',
    label: 'Horarios',
    field: 'horario',
    sortable: true
  },
  {
    name: 'opciones',
    label: 'Opciones',
    field: 'opciones'
  }
];

async function ObtenerDatos() {
  try {
    const response = await axios.get('https://transporte-0ydp.onrender.com/api/transporte/transbusca');
    guardardatos.value = response.data.transporte.map(transporte => ({
      numero_asiento: transporte.NumAsientos,
      vehiculo: transporte.Vehiculo,
      horario: transporte.horario,
      opciones: '<button @click="eliminarFila">Eliminar</button> <button @click="editarFila">Editar</button>'
    }));
  } catch (error) {
    console.error('Error al obtener datos:', error);
  }
}

onMounted(() => {
  ObtenerDatos();
});

</script>



<style scoped>
.body {
  display: flex;

  flex-direction: column;
  align-items: center;
  text-align: center;
  height: 100vh;
  background-color: #ffffff;
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: rgba(0, 0, 0, 0.87);
  /* font-synthesis: none; */
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
  margin-top: 10%;
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
  background-color: rgb(119, 119, 119);
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