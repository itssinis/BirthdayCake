<template>
  <div class="flex flex-col items-center justify-center w-full h-screen bg-[#bcf1e7]">
    <div class="relative w-[600px] h-[450px] flex justify-center items-center">
      <!-- Imagen del sobre -->
      <img
        :src="mostrarCarta ? sobreAbierto : sobreSellado"
        class="w-full h-auto transition-all duration-500"
      />
    </div>

    <!-- Carta -->
    <div
      v-if="mostrarCarta"
      class="mt-4 w-[280px] bg-white rounded-md shadow-lg p-4 text-center animate-aparecer"
    >
      <p class="text-gray-800 font-medium text-lg">
        ¡Feliz cumpleaños! 🎉 Te quiero mucho. 💛
      </p>
    </div>

    <!-- Botón -->
    <button
      @click="alternarCarta"
      class="mt-6 px-4 py-2 bg-yellow-400 text-white font-semibold rounded shadow hover:bg-yellow-500 transition"
    >
      {{ mostrarCarta ? 'Cerrar carta' : 'Abrir carta' }}
    </button>
  </div>
</template>

<script>
import sobreSellado from '../assets/images/sobre-sellado.png';
import sobreAbierto from '../assets/images/sobre-abierto.png';

export default {
  data() {
    return {
      mostrarCarta: false,
      sobreSellado,
      sobreAbierto
    };
  },
  methods: {
    alternarCarta() {
      this.mostrarCarta = !this.mostrarCarta;
    }
  }
};
</script>

<style scoped>
@keyframes aparecer {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
.animate-aparecer {
  animation: aparecer 1s ease-out forwards;
}
</style>
