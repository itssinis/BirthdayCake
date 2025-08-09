<template>
  <div class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50">
    <div class="relative bg-white p-4 rounded-lg shadow-lg w-full max-w-[90vw] h-full max-h-[90vh] overflow-hidden">
      
      <!-- Botón cerrar -->
       <button>
        <i
          class="close-btn fa-solid fa-times absolute top-2 right-2 text-gray-500 hover:text-red-500 cursor-pointer z-50"
          @click="cerrarAlbum"
          title="Cerrar álbum"
        ></i>
      </button>

      <!-- Contenedor del álbum -->
      <div ref="album" class="album-container mx-auto"></div>
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
  data() {
    return {
      singlePageMode: false
    };
  },
  methods: {
    cerrarAlbum() {
      console.log('Botón cerrar clickeado'); // Para debugging
      try {
        this.destroyTurn();
        this.$emit('cerrar');
      } catch (error) {
        console.error('Error al cerrar álbum:', error);
        this.$emit('cerrar'); // Emitir de todas formas
      }
    },

    /** Detecta si debe ir en single o double page */
    checkSinglePageMode() {
      const isPortrait = window.innerHeight > window.innerWidth;
      const isSmallScreen = window.innerWidth < 768; // breakpoint tablet

      // En portrait o pantallas pequeñas → single page
      this.singlePageMode = isPortrait || isSmallScreen;
    },

    /** Inicia el libro */
    initTurn() {
      const albumElement = window.$(this.$refs.album);
      albumElement.html('');

      const pageWidth = Math.min(window.innerWidth * 0.9, 800);
      const pageHeight = Math.min(window.innerHeight * 0.8, 600);

      albumElement.turn({
        width: pageWidth,
        height: pageHeight,
        autoCenter: true,
        display: this.singlePageMode ? 'single' : 'double'
      });

      // Cargar páginas
      this.fotos.forEach((pagina, index) => {
        const page = document.createElement('div');
        page.classList.add('p-2', 'flex', 'items-center', 'justify-center');

        if (pagina.tipo === 'imagen') {
          const img = document.createElement('img');
          img.src = pagina.contenido;
          img.classList.add('max-w-full', 'max-h-full', 'rounded-lg');
          page.appendChild(img);
        }

        if (pagina.tipo === 'doble') {
          const container = document.createElement('div');
          container.classList.add('grid', 'grid-cols-2', 'gap-1', 'w-full', 'h-full');
          pagina.contenido.forEach(url => {
            const img = document.createElement('img');
            img.src = url;
            img.classList.add('w-full', 'h-full', 'object-contain', 'rounded-lg');
            container.appendChild(img);
          });
          page.appendChild(container);
        }

        if (pagina.tipo === 'texto') {
          const p = document.createElement('p');
          p.textContent = pagina.contenido;
          p.classList.add('text-center', 'text-sm', 'sm:text-lg', 'font-medium');
          page.appendChild(p);
        }

        if (pagina.tipo === 'mixto') {
          const container = document.createElement('div');
          container.classList.add('flex', 'flex-col', 'items-center', 'gap-2', 'w-full', 'h-full');

          const img = document.createElement('img');
          img.src = pagina.contenido.imagen;
          img.classList.add('max-w-full', 'max-h-[70%]', 'rounded-lg');

          const p = document.createElement('p');
          p.textContent = pagina.contenido.texto;
          p.classList.add('text-center', 'text-xs', 'sm:text-base');

          container.appendChild(img);
          container.appendChild(p);
          page.appendChild(container);
        }

        albumElement.turn('addPage', page, index + 1);
      });
    },

    /** Elimina el libro para reiniciarlo */
    destroyTurn() {
      if (this.$refs.album && window.$(this.$refs.album).data('turn')) {
        window.$(this.$refs.album).turn('destroy').remove();
      }
    },

    /** Recalcula en resize/orientación */
    handleResize() {
      this.checkSinglePageMode();
      this.destroyTurn();
      this.initTurn();
    }
  },
  mounted() {
    this.checkSinglePageMode();
    this.initTurn();
    window.addEventListener('resize', this.handleResize);
    window.addEventListener('orientationchange', this.handleResize);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
    window.removeEventListener('orientationchange', this.handleResize);
    this.destroyTurn();
  }
};
</script>

<style scoped>
.album-container {
  transition: all 0.3s ease;
}

@media (max-width: 768px) {
  .album-container {
    transform: scale(0.95);
    transform-origin: top center;
  }
}
</style>
