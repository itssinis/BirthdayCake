<template>
  <div class="flex flex-col items-center justify-center w-full h-screen bg-[#bcf1e7] relative">
    <div class="relative w-[600px] h-[450px] flex justify-center items-center">
      <!-- Imagen del sobre -->
      <img
        :src="mostrarCarta ? sobreAbierto : sobreSellado"
        class="w-full h-auto transition-all duration-500"
      />

      <!-- Carta -->
      <div
        v-if="mostrarCarta"
        class="absolute top-[-90px] w-[570px] bg-white p-6 shadow-lg rounded-lg z-20 animate-aparecer"
      >
        <!-- X de cerrar -->
        <i
          class="fa-solid fa-times absolute top-3 right-3 text-gray-500 hover:text-red-500 cursor-pointer"
          @click="mostrarCarta = false"
        ></i>

        <p class="text-gray-800 font-medium text-lg leading-relaxed">
          Hola, mi amor.<br />
          ¡Feliz cumpleaños! Bienvenida al segundo piso, espero hoy puedas pasar un día muy bonito, preciosa. Te amo, ¿lo sabías? 
          Agradezco demasiado el poder compartir mi vida contigo, y tengo la seguridad de que lo seguiremos haciendo por años. <br /><br />
          Has pasado 20 años siendo la mujer más increíble, hermosa, inteligente, adorable, tierna, valiente, de todo el universo 
          (sé que dirás que no, pero sí lo eres, para mí lo eres). Han sido 20 años en los que has vivido muchas aventuras, 
          en los que has reído, llorado, te has enojado, has sido muy feliz en muchas ocasiones (espero que en la mayoría), 
          dónde has tenido diferentes mascotas, dónde cumpliste sueños, tuviste muchos logros y dónde has impactado de una manera 
          u otra la vida de muchas personas, yo soy una de ellas. Una lastima es que ya no puedas identificarte con “Antes de los 20” 
          pero es parte de. <br /><br />
          De los 20 que estás cumpliendo hoy, he estado contigo en 3, y espero estarlo por el resto de tu vida si me lo permites. <br /><br />
          Te amo, con toda el alma. <br />
          Con amor, S.
        </p>
      </div>
    </div>

    <!-- Botones -->
    <div class="mt-6 flex gap-4">
      <button
        @click="mostrarCarta = true"
        v-if="!mostrarCarta"
        class="px-4 py-2 bg-[#185D51] text-white font-semibold rounded shadow hover:bg-[#26806f] transition"
      >
        Abrir carta
      </button>

      <button
        @click="abrirAlbum"
        class="px-4 py-2 bg-[#185D51] text-white font-semibold rounded shadow hover:bg-[#26806f] transition"
      >
        Ver álbum
      </button>
    </div>
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
    abrirAlbum() {
      alert('Aquí se abriría el álbum 📸');
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
  animation: aparecer 0.6s ease-out forwards;
}
</style>
