<template>
  <div
    class="flex flex-col items-center justify-center w-full min-h-screen bg-[#bcf1e7] relative p-4 lg:p-0"
  >
    <!-- Contenedor principal responsivo -->
    <div class="flex flex-col lg:flex-row items-center justify-center gap-6 w-full max-w-6xl">
      
      <!-- Imágenes izquierda -->
      <div class="flex gap-3 lg:flex-col lg:gap-7 mb-4 lg:mb-0 lg:mx-12">
        <img
          v-for="(img, i) in imagenesIzquierda"
          :key="i"
          :src="img"
          alt=""
          class="w-20 sm:w-24 lg:w-[190px] h-auto animate-float"
        />
      </div>

      <!-- Sobre y carta -->
      <div class="relative flex flex-col items-center w-full max-w-[600px]">
        <img
          :src="mostrarCarta ? sobreAbierto : sobreSellado"
          class="w-full max-w-[600px] h-auto transition-all duration-500"
        />

        <!-- Carta -->
        <div
        v-if="mostrarCarta"
        class="absolute top-[-90px] w-[95%] max-w-[570px] bg-white p-6 shadow-lg rounded-lg z-20 animate-aparecer lg:max-h-[99vh] max-h-[70vh] overflow-y-auto"
      >
          <!-- Botón cerrar -->
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

        <!-- Botón abrir carta -->
        <div class="mt-4">
          <button
            @click="mostrarCarta = true"
            v-if="!mostrarCarta"
            class="px-4 py-2 bg-[#185D51] text-white font-semibold rounded shadow hover:bg-[#26806f] transition text-sm sm:text-base"
          >
            Abrir carta
          </button>
        </div>
      </div>

      <!-- Imágenes derecha -->
      <div class="flex gap-3 lg:flex-col lg:gap-7 mt-4 lg:mt-0 lg:mx-12">
    <img
      v-for="(img, i) in imagenesDerecha"
      :key="i"
      :src="img"
      alt=""
      class="w-20 sm:w-24 lg:w-[190px] h-auto animate-float"
    />
  </div>
    </div>
  </div>
</template>

<script>
import sobreSellado from "../assets/images/sobre-sellado.png";
import sobreAbierto from "../assets/images/sobre-abierto.png";
import ilustracion1 from "../assets/images/juntas.png";
import ilustracion2 from "../assets/images/cine.png";
import ilustracion3 from "../assets/images/flor.png";
import ilustracion4 from "../assets/images/beso.png";
import ilustracion5 from "../assets/images/caminando.png";
import ilustracion6 from "../assets/images/dormida.png";

export default {
  data() {
    return {
      mostrarCarta: false,
      sobreSellado,
      sobreAbierto,
      imagenesIzquierda: [ilustracion1, ilustracion2, ilustracion3],
      imagenesDerecha: [ilustracion4, ilustracion5, ilustracion6],
    };
  },
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

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}
.animate-float {
  animation: float 4s ease-in-out infinite;
}
</style>

