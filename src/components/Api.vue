<script setup>
import { onMounted,ref } from 'vue';
const info = ref ('');
async function fetchData() {
try {
const response = await fetch('https:/sitmotul.com.mx/api/statusEval');
const data = await response.json();
info.value=data;
console.log (info.value)
}catch (error) {
 console.error('Error al obtener datos:', error);
  }
}

onMounted(() => {
fetchData();
})
import Tiempo from './Tiempo.vue'
import Total from './Total.vue'
</script>

<template>
 <div class="contenedor-transparente">
  <div class="boton">
  <a href="#" class="active">Ingeniería Industrial</a>
  <a href="#">Ingeniería de Energias Renobables</a>
  <a href="#">Ingeniería en Sistemas Computacionales</a>
  <a href="#">Ingeniería en Electronica</a>
  <a href="#">Ingeniería en Electromecánica</a>
</div>
 </div>


 <div class="contenedor">
<Tiempo></Tiempo>
 </div>

 <div class="cont">
  <Total></Total>
 </div>

</template>