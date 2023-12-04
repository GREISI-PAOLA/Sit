
<template>
 <div id="app">
    <div class="container">
      <div v-for="(data, index) in infoPersonal" :key="index" class="item" @mouseover="hoverItem" @mouseout="unhoverItem">
        <div v-if="data.IEM">
          <p>Ingenieria en Electromécanica</p>
          <p>Listas: {{ data.IEM.listas }}</p>
          <p>Faltantes: {{ data.IEM.faltantes }}</p>
        </div>
      </div>

      <div v-for="(data, index) in infoPersonal" :key="index" class="item" @mouseover="hoverItem" @mouseout="unhoverItem">
        <div v-if="data.IER">
          <p>Ingenieria en Energías Renobables</p>
            <p>Listas: {{ data.IER.listas }}</p> 
          <p> Faltantes: {{ data.IER.faltantes }}</p>
        </div>
      </div>

      <div v-for="(data, index) in infoPersonal" :key="index" class="item" @mouseover="hoverItem" @mouseout="unhoverItem">
        <div v-if="data.II">
          <p>Ingeniria Industrial</p>
          <p>Listas: {{ data.II.listas }}</p>
          <p>Faltantes: {{ data.II.faltantes }}</p>
        </div>
      </div>

      <div v-for="(data, index) in infoPersonal" :key="index" class="item" @mouseover="hoverItem" @mouseout="unhoverItem">
        <div v-if="data.ISC">
          <p>Ingenieria en Sistemas Computacionales </p>
          <p> Listas: {{ data.ISC.listas }}</p>
          <p> Faltantes: {{ data.ISC.faltantes }}</p>
        </div>
      </div>

      <div v-for="(data, index) in infoPersonal" :key="index" class="item" @mouseover="hoverItem" @mouseout="unhoverItem">
        <div v-if="data.IE">
          <p>Ingenieria en Electrónica</p>
          <p >Listas: {{ data.ISC.listas }}</p>
            <p> Faltantes: {{ data.IE.faltantes }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import { ref } from 'vue'

// Definir variables reactivas
const infoGeneral = ref([]) // Almacena datos de Información General
const infoPersonal = ref([]) // Almacena datos de Información Personal

// Variables para mostrar en la plantilla
const totalEvaluados = ref(0)
const totalAlumnos = ref(0)
const periodo = ref('')

// Función para obtener datos de la API
async function fetchData(apiUrl, infoArray) {
	try {
		const response = await fetch(apiUrl)
		const data = await response.json()
		infoArray.value.push(data) // Almacenar datos en el array correspondiente

		// Actualizar variables para mostrar en la plantilla
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

const hoverItem = (event) => {
  event.target.style.backgroundColor = '#84da33';
};

const unhoverItem = (event) => {
  event.target.style.backgroundColor = 'transparent';
};



</script>