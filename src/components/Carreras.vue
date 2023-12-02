<script setup>

import { onMounted } from 'vue';
import { ref } from 'vue';

const infoi = ref('');
var IEML = "";
var IEMF = "";
var IIL = "";
var IIF = "";
var ISCL = "";
var ISCF = "";
var IEL = "";
var IEF = "";
var IERL = "";
var IERF= "";

async function fetchData() {
  try {
    const response = await fetch('https://sitmotul.com.mx/api/statusEvalIng')
    const data = await response.json();
    infoi.value = data
    // isLoading.value = false

    // IEM
    IEML = infoi.value['IEM'] ['listas'];
    IEMF = infoi.value['IEM'] ['faltantes'];
    document.getElementById('IEML').textContent = "Al día de hoy se han realizado " + IEML + " evaluaciones";
    document.getElementById('IEMF').textContent = "Faltan por realizarse " + IEMF + " evaluaciones";

    //II
    IIL = infoi.value['II'] ['listas'];
    IIF = infoi.value['II'] ['faltantes'];
    document.getElementById('IIL').textContent = "Al día de hoy se han realizado " + IIL + " evaluaciones";
    document.getElementById('IIF').textContent = "Faltan por realizarse " + IIF + " evaluaciones";

    //ISC
    ISCL = infoi.value['ISC'] ['listas'];
    ISCF = infoi.value['ISC'] ['faltantes'];
    document.getElementById('ISCL').textContent = "Al día de hoy se han realizado " + ISCL + " evaluaciones";
    document.getElementById('ISCF').textContent = "Faltan por realizarse " + ISCF + " evaluaciones";

    //IER
    IERL = infoi.value['IER'] ['listas'];
    IERF = infoi.value['IER'] ['faltantes'];
    document.getElementById('IERL').textContent = "Al día de hoy se han realizado " + IERL + " evaluaciones";
    document.getElementById('IERF').textContent = "Faltan por realizarse " + IERF + " evaluaciones";

   //IE
    IEL = infoi.value['IE'] ['listas'];
    IEF = infoi.value['IE'] ['faltantes'];
    document.getElementById('IEL').textContent = "Al día de hoy se han realizado " + IEL + " evaluaciones";
    document.getElementById('IEF').textContent = "Faltan por realizarse " + IEF + " evaluaciones";

    console.log(IEML);
  } catch (error) {
    console.error('Error al obtener datos:', error);
  }
}

onMounted(() => {
  fetchData();
})

</script>
<template>

</template>