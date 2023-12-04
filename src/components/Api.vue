<script setup>
import { onMounted, ref, defineProps } from 'vue';

const info = ref('');

const emitirSeleccion = (pestaña) => {
  emit('seleccionarPestana', pestaña);
};

async function fetchData() {
  try {
    const response = await fetch('https://sitmotul.com.mx/api/statusEval');
    const data = await response.json();
    info.value = data;
    console.log(info.value);
  } catch (error) {
    console.error('Error al obtener datos:', error);
  }
}



onMounted(() => {
  fetchData();
});
import Tiempo from './Tiempo.vue'
import Total from './Total.vue'
import Carreras from './Carreras.vue'
</script>

<template>
  <div class="contenedores-flex">
 <div class="contenedor-transparente">
      <div class="boton">
      <Carreras></Carreras>
      </div>
      </div>
    </div>

 <div class="contenedores-flex">
 <div class="contenedor">
<Tiempo></Tiempo>
 </div>

 <div class="cont">
  <Total></Total>
 </div>

 <div>
  
</div>
 </div>

</template>