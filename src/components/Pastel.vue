<template>
  <div class="h-screen w-screen bg-[#C6F0E9] flex flex-col justify-between overflow-hidden">
    <!-- Encabezado -->
    <header class="pt-12 px-6 text-center">
      <h1 class="text-5xl md:text-6xl font-extrabold leading-tight text-[#000000]">
        ¡Feliz cumpleaños, mi amor! 
      </h1>
    </header>

    <!-- Centro: Pastel -->
    <main class="flex-grow flex items-center justify-center">
      <div class="relative">
        <!-- Plato base -->
        <div class="w-80 h-6 bg-gradient-to-b from-gray-300 to-gray-400 rounded-full shadow-xl absolute -bottom-3 left-1/2 transform -translate-x-1/2 opacity-60"></div>
        
        <!-- Cuerpo del pastel -->
        <div class="w-72 h-32 bg-gradient-to-b bg-[#D9D9D9] shadow-2xl relative rounded-2xl">
          <!-- Textura del pastel -->
          <div class="absolute inset-0 bg-gradient-to-r from-transparent via-white/10 to-transparent rounded-2xl"></div>
        </div>

        <!-- Frosting superior -->
        <div class="absolute -top-2 left-0 right-0">
          <div class="w-72 h-6 bg-gradient-to-b bg-[#966969] relative rounded-t-2xl">
            <!-- Borde ondulado del frosting -->
            <div class="absolute -bottom-3 left-0 right-0 flex">
              <div
                v-for="i in 8"
                :key="i"
                class="flex-1 h-3 bg-[#966969] rounded-b-full"
                :style="{ marginLeft: i > 1 ? '-1px' : '0' }"
              ></div>
            </div>
          </div>
        </div>

        <!-- Velas -->
        <div class="absolute -top-12 left-1/2 transform -translate-x-1/2 flex gap-12">
          <div
            v-for="(lit, i) in velasEncendidas"
            :key="i"
            class="relative"
          >
            <!-- Vela -->
            <div class="w-3 h-14 bg-gradient-to-b from-yellow-100 to-yellow-200 rounded-sm shadow-md border border-yellow-300"></div>

            <!-- Llama -->
            <div v-if="lit" class="absolute -top-4 left-1/2 transform -translate-x-1/2">
              <div class="relative">
                <!-- Resplandor exterior -->
                <div class="absolute inset-0 w-6 h-6 bg-orange-300 rounded-full blur-md opacity-40 animate-pulse" style="animation-duration: 1.5s;"></div>
                <!-- Resplandor medio -->
                <div class="absolute inset-0 w-4 h-5 bg-yellow-300 rounded-full blur-sm opacity-70 animate-pulse" style="animation-duration: 1.2s;"></div>
                <!-- Llama principal con movimiento ondulante -->
                <div
                  class="w-3 h-4 bg-gradient-to-t from-orange-600 via-orange-400 to-yellow-300 rounded-full"
                  style="animation: flame-flicker 0.5s ease-in-out infinite alternate;"
                ></div>
              </div>
            </div>

            <!-- Efecto de humo cuando se apaga -->
            <div v-if="!lit" class="absolute -top-3 left-1/2 transform -translate-x-1/2">
              <div class="relative">
                <!-- Múltiples líneas de humo con animación mejorada -->
                <div
                  class="w-0.5 h-8 bg-gradient-to-t from-gray-500 via-gray-300 to-transparent opacity-60"
                  style="animation: smoke-rise 3s ease-out infinite;"
                ></div>
                <div
                  class="absolute -left-1 top-2 w-0.5 h-6 bg-gradient-to-t from-gray-400 via-gray-200 to-transparent opacity-40"
                  style="animation: smoke-rise 3.5s ease-out infinite; animation-delay: 0.4s;"
                ></div>
                <div
                  class="absolute left-1 top-1 w-0.5 h-7 bg-gradient-to-t from-gray-500 via-gray-200 to-transparent opacity-50"
                  style="animation: smoke-rise 2.8s ease-out infinite; animation-delay: 0.8s;"
                ></div>
                <!-- Partículas de humo adicionales -->
                <div
                  class="absolute -left-0.5 top-4 w-0.5 h-4 bg-gradient-to-t from-gray-300 to-transparent opacity-30"
                  style="animation: smoke-rise 4s ease-out infinite; animation-delay: 1.2s;"
                ></div>
                <div
                  class="absolute left-0.5 top-3 w-0.5 h-5 bg-gradient-to-t from-gray-400 to-transparent opacity-35"
                  style="animation: smoke-rise 3.2s ease-out infinite; animation-delay: 1.6s;"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Botón abajo -->
    <footer class="pb-12 text-center">
      <button
        class="px-8 py-4 bg-[#185D51] text-white text-xl font-bold rounded-full shadow-lg hover:bg-[#34CBAF] transition-all duration-300 transform hover:scale-105"
        @click="iniciarMicrofono"
      >
        Sopla para apagar las velas
      </button>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      velasEncendidas: [true, true, true],
      escuchando: false,
      stream: null
    };
  },
  methods: {
    async iniciarMicrofono() {
      try {
        this.stream = await navigator.mediaDevices.getUserMedia({ audio: true });
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        const mic = audioContext.createMediaStreamSource(this.stream);
        const analyser = audioContext.createAnalyser();
        mic.connect(analyser);

        const dataArray = new Uint8Array(analyser.fftSize);
        this.escuchando = true;

        const detectarSoplo = () => {
          analyser.getByteTimeDomainData(dataArray);
          const volumen = Math.max(...dataArray) - Math.min(...dataArray);

          if (volumen > 50) {
            this.velasEncendidas = this.velasEncendidas.map(() => false);
            this.escuchando = false;
            this.stream.getTracks().forEach(t => t.stop());
          }

          if (this.escuchando) requestAnimationFrame(detectarSoplo);
        };

        detectarSoplo();
      } catch (err) {
        alert("No se pudo acceder al micrófono 😢");
        console.error(err);
      }
    }
  }
};
</script>

<style scoped>
@keyframes flame-flicker {
  0% { transform: scale(1) rotate(-1deg); }
  50% { transform: scale(1.05) rotate(1deg); }
  100% { transform: scale(0.98) rotate(-0.5deg); }
}

@keyframes flame-inner {
  0% { opacity: 0.8; transform: translateX(-50%) scale(1); }
  50% { opacity: 0.9; transform: translateX(-50%) scale(1.1); }
  100% { opacity: 0.7; transform: translateX(-50%) scale(0.9); }
}

@keyframes sparkle {
  0% { opacity: 0.9; transform: translateX(-50%) scale(1); }
  50% { opacity: 1; transform: translateX(-50%) scale(1.2); }
  100% { opacity: 0.8; transform: translateX(-50%) scale(0.8); }
}

@keyframes smoke-rise {
  0% { 
    opacity: 0.6; 
    transform: translateY(0) translateX(0) scale(1); 
  }
  50% { 
    opacity: 0.4; 
    transform: translateY(-10px) translateX(2px) scale(1.1); 
  }
  100% { 
    opacity: 0.1; 
    transform: translateY(-20px) translateX(-1px) scale(1.2); 
  }
}
</style>
