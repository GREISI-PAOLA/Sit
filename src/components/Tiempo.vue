
<script setup>
import { ref, onMounted } from 'vue';

const fechaLimite = new Date('2023-12-05T00:00:00');

const dias = ref(0);
const minutos = ref(0);
const segundos = ref(0);

const actualizarTiempo = () => {
  const fechaActual = new Date();
  const diferenciaMs = fechaLimite - fechaActual;

  dias.value = Math.floor(diferenciaMs / (1000 * 60 * 60 * 24));
  minutos.value = Math.floor((diferenciaMs % (1000 * 60 * 60 * 24)) / (1000 * 60));
  segundos.value = Math.floor((diferenciaMs % (1000 * 60)) / 1000);
};

onMounted(() => {
  actualizarTiempo();
  setInterval(actualizarTiempo, 1000); // Actualizar cada segundo
});
</script>

<template>
  <div id="resultado-container" class="contenedor">
    <div class="tiempo">
      <div class="conteT">
        <div>
      <span class="dias">Días: {{ dias }}</span>
    </div>
    <div>
      <span class="minutos">Minutos: {{ minutos }}</span>
    </div>
    <div>
      <span class="segundos">Segundos: {{ segundos }}</span>
    </div>
    </div>
  </div>
</div>


</template>
