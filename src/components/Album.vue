<template>
  <div
    class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50"
  >
    <div class="relative bg-white p-4 rounded-lg shadow-lg">
      <!-- Botón cerrar -->
      <i
        class="fa-solid fa-times absolute top-2 right-2 text-gray-500 hover:text-red-500 cursor-pointer z-50"
        @click="cerrarAlbum"
      ></i>

      <!-- Cuaderno -->
      <div ref="album" class="w-[600px] h-[400px]"></div>
    </div>
  </div>
</template>

<script>
import 'turn.js';

export default {
  name: 'Album',
  props: {
    fotos: {
      type: Array,
      required: true
    }
  },
  methods: {
    cerrarAlbum() {
      console.log('Cerrar emitido'); // Debug
      this.$emit('cerrar');
    }
  },
  mounted() {
    window.$(this.$refs.album).turn({
      width: 600,
      height: 400,
      autoCenter: true,
      pages: this.fotos.length
    });

    this.fotos.forEach((foto, index) => {
      const page = document.createElement('div');
      page.classList.add('p-4', 'flex', 'items-center', 'justify-center');
      const img = document.createElement('img');
      img.src = foto;
      img.classList.add('max-w-full', 'max-h-full', 'rounded-lg');
      page.appendChild(img);
      window.$(this.$refs.album).turn('addPage', page, index + 1);
    });
  }
};
</script>
