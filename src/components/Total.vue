<template>
  <div class="contenedores-flex">
	<div id="resultadocontainer" class="resultadocontenedor">
			<div class="resulT">
        <div v-for="(data, index) in infoGeneral" :key="index" >
          
            <p> {{ calcularPorcentaje(data.alEvaluados, data.alTotal) }} % </p>
            <p>Han contestado {{ totalEvaluados }} alumnos de un total de {{ totalAlumnos }} alumnos</p>
          </div>
		</div>
	</div>

<div id="resultadocontainer2" class="resultadocontenedor2">
			<div class="resulT2">
        <div v-for="(data, index) in infoGeneral" :key="index">
            <p> {{ calcularPorcentajeFaltante(data.alEvaluados, data.alTotal) }} % </p>
						<p>	No han contestado {{ data.alTotal - data.alEvaluados }} alumnos de {{ data.alTotal }}</p>
		</div>
	</div>
	</div>
</div>

</template>

<script setup>
import { onMounted } from 'vue'
import { ref } from 'vue'

// Definir variables reactivas
const infoGeneral = ref([]) 
const infoPersonal = ref([]) 

// Variables 
const totalEvaluados = ref(0)
const totalAlumnos = ref(0)
const periodo = ref('')

// Función para obtener datos de la API
async function fetchData(apiUrl, infoArray) {
	try {
		const response = await fetch(apiUrl)
		const data = await response.json()
		infoArray.value.push(data) 

		// Actualizar variables
		totalEvaluados.value += data.alEvaluados || 0
		totalAlumnos.value += data.alTotal || 0
		if (!periodo.value) {
			periodo.value = data.periodo || ''
		}

		console.log('Datos recibidos:', data)
		// Imprimir datos adicionales en la consola
		if (data.ObjectIE) {
			console.log('ObjectIE:', data.ObjectIE)
		}
		if (data.IEM) {
			console.log('IEM:', data.IEM)
		}
		if (data.IER) {
			console.log('IER:', data.IER)
		}
		if (data.II) {
			console.log('II:', data.II)
		}
		if (data.ISC) {
			console.log('ISC:', data.ISC)
		}
	} catch (error) {
		console.error('Error al obtener datos:', error)
	}
}

// Función que se ejecuta al montar el componente
onMounted(async () => {
	// Obtener datos de la primera API
	await fetchData('https://sitmotul.com.mx/api/statusEval', infoGeneral)

	// Obtener datos de la segunda API (puedes cambiar la URL según sea necesario)
	await fetchData('https://sitmotul.com.mx/api/statusEvalIng', infoPersonal)
})

// Función para calcular el porcentaje
const calcularPorcentaje = (evaluados, total) => {
	if (total === 0) {
		return 0;
	}
	return ((evaluados / total) * 100).toFixed(2);
};

// Función para calcular el porcentaje de los evaluados que faltan
const calcularPorcentajeFaltante = (evaluados, total) => {
	const faltantes = total - evaluados;
	if (total === 0 || faltantes <= 0) {
		return 0;
	}
	return ((faltantes / total) * 100).toFixed(2);
};
</script>

