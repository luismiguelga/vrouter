<template>
  <div class="body">
    <div class="tabla">
      <h1>Tabla</h1>
      <table>
        <thead>
          <tr>
            <th>Codigo</th>
            <th>Nombre</th>
            <th>Cantidad</th>
            <th>Precio</th>
            <th>Costo</th>
            <th>Precio Total</th>
            <th>Costo Total</th>
            <th>Ganancias</th>
            <th>Opciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(dato, index) in data" :key="index">
            <td>{{ dato.codigo }}</td>
            <td>{{ dato.nombre }}</td>
            <td :style="cambiarcolor(dato.cantidad)">{{ dato.cantidad }}</td>
            <td>{{ dato.precio }}</td>
            <td>{{ dato.costo }}</td>
            <td>{{ dato.precio * dato.cantidad }}</td>
            <td>{{ dato.costo * dato.cantidad }}</td>
            <td>{{ (dato.precio * dato.cantidad) - (dato.costo * dato.cantidad) }}</td>
            <td>
              <button @click="eliminar(index)" id="eliminar">❌</button>
              <button @click="editar(dato, index)" id="editar" data-bs-toggle="modal"
                data-bs-target="#exampleModal">📋</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
  

<script setup>
import { ref } from 'vue';

const codigo = ref('');
const nombre = ref('');
const cantidad = ref(0);
const precio = ref(0);
const costo = ref(0);
let boton = ref("Agregar")
const data = ref([
  { codigo: "001", nombre: "Shampoo", cantidad: 1, precio: 10, costo: 5 }
]);
let indiceEdicion = ref(-1); // Agrega una referencia para almacenar el índice del producto en edición
const alerta1 = ref('');
const alerta2 = ref('');
const alerta3 = ref('');
const alerta4 = ref('');
const alerta5 = ref('');

function agregarFila() {
  if(validar()){
  if (boton.value === "Editar") {
    if (indiceEdicion.value >= 0) {
      // Editar un producto existente
      const productoEditado = {
        codigo: codigo.value,
        nombre: nombre.value,
        cantidad: cantidad.value,
        precio: precio.value,
        costo: costo.value,
      };
      data.value.splice(indiceEdicion.value, 1, productoEditado);
      boton.value = "Agregar";
    }
  } else {
    // Agregar un nuevo producto
    const nuevoProducto = {
      codigo: codigo.value,
      nombre: nombre.value,
      cantidad: cantidad.value,
      precio: precio.value,
      costo: costo.value,
    };
    data.value.push(nuevoProducto);
    limpiar();
  }
}
}

function validar(){
  let validacion = true;
  if (!codigo.value) {
      alerta1.value = "Por favor, digite código"
      al.style.color = "Orange"
      al.style.fontSize = "30px"
      al.style.fontWeight = "Bolder"
      setTimeout(function () {
        alerta1.value = "";
        alerta1.style = "";
      }, 2500)
      validacion = false;
    ;
   
  } else if (!nombre.value) {
      alerta2.value = "Por favor, digite nombre"
      ale.style.color = "Orange"
      ale.style.fontSize = "30px"
      ale.style.fontWeight = "Bolder"
      setTimeout(function () {
        alerta2.value = "";
        alerta2.style = "";
      }, 2500)
      validacion = false;
    
  } else if (!cantidad.value) {
      alerta3.value = "Por favor, digite una cantidad mayor a 0"
      aler.style.color = "Orange"
      aler.style.fontSize = "30px"
      aler.style.fontWeight = "Bolder"
      setTimeout(function () {
        alerta3.value = "";
        alerta3.style = "";
      }, 2500)
      validacion = false;
    
  } else if (!precio.value) {

      alerta4.value = "Por favor, digite un precio mayor a 0"
      alertt.style.color = "Orange"
      alertt.style.fontSize = "30px"
      alertt.style.fontWeight = "Bolder"
      setTimeout(function () {
        alerta4.value = "";
        alerta4.style = "";
      }, 2500)
      validacion = false;
  } else if (!costo.value) {

      alerta5.value = "Por favor, digite un costo mayor a 0"
      alerta.style.color = "Orange"
      alerta.style.fontSize = "30px"
      alerta.style.fontWeight = "Bolder"
      setTimeout(function () {
        alerta5.value = "";
        alerta5.style = "";
      }, 2500)
      validacion = false;
    
  } else if (costo.value>precio.value) {
      alerta5.value = "El costo no puede ser mayor a el precio del producto"
      alerta.style.color = "Orange"
      alerta.style.fontSize = "30px"
      alerta.style.fontWeight = "Bolder"
      setTimeout(function () {
        alerta5.value = "";
        alerta5.style = "";
      }, 2500)
      validacion = false;

  }else{
      alerta5.value = "Datos guardados exitosamente, por favor presione click en 'Cerrar'"
      alerta.style.color = "Green"
      alerta.style.fontSize = "30px"
      alerta.style.fontWeight = "Bolder"
      setTimeout(function () {
        alerta5.value = "";
        alerta5.style = "";
      }, 3500)
      validacion = false;
  }
  return validacion
}

function cambiarcolor(cantidadValue) {
  if (cantidadValue < 10) {
    return { color: 'red' };
  } else if (cantidadValue > 50) {
    return { color: 'blue' };
  } else {
    return { color: 'black' };
  }
}
function limpiar() {
  codigo.value = "";
  nombre.value = "";
  cantidad.value = 0;
  precio.value = 0;
  costo.value = 0;
}

function eliminar(index) {
  data.value.splice(index, 1)
}
function editar(dato, index) {
  codigo.value = dato.codigo
  nombre.value = dato.nombre
  cantidad.value = dato.cantidad
  precio.value = dato.precio
  costo.value = dato.costo
  boton.value = "Editar"
  indiceEdicion.value = index; // Almacena el índice del producto en edición
}

async function Obenerinfortransporte(pokemon) {
  const response = await axios.get(`https://transporte-0ydp.onrender.com/api/asiento/asientobusca`)
}

onMounted(() => {
  Obenerinfortransporte()
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