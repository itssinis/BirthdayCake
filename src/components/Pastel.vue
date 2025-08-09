<template>
  <div class="h-screen w-screen bg-[#bcf1e7] flex flex-col justify-between overflow-hidden">
    <!-- Encabezado -->
    <header class="pt-12 px-6 text-center">
      <h1 class="text-5xl md:text-6xl font-extrabold leading-tight text-[#000000]">
        ¡Feliz cumpleaños, mi amor! 
      </h1>
    </header>

    <!-- Centro: Pastel -->
    <main class="flex-grow flex items-center justify-center ">
      <div class="relative">
        <!-- Plato base -->
        <div class="w-72 h-6 bg-gradient-to-b from-gray-300 to-gray-400 rounded-full shadow-xl absolute -bottom-3 left-1/2 transform -translate-x-1/2 opacity-60"></div>
        
        <!-- Cuerpo del pastel -->
        <div class="w-60 h-32 bg-gradient-to-b bg-[#D9D9D9] shadow-2xl relative rounded-2xl">
          <!-- Textura del pastel -->
          <div class="absolute inset-0 bg-gradient-to-r from-transparent via-white/10 to-transparent rounded-2xl"></div>
        </div>

        <!-- Frosting superior -->
        <div class="absolute -top-2 left-0 right-0">
          <div class="w-75 h-12 bg-gradient-to-b bg-[#966969] relative rounded-t-2xl">
            <!-- Sprinkles -->
            <div class="absolute inset-0 pointer-events-none">
              <div class="w-1 h-1 bg-blue-400 rounded-full absolute top-3 left-6"></div>
              <div class="w-1 h-1 bg-yellow-300 rounded-full absolute top-4 left-20"></div>
              <div class="w-1 h-1 bg-red-400 rounded-full absolute top-2 left-32"></div>
              <div class="w-1 h-1 bg-green-300 rounded-full absolute top-5 left-10 "></div>
              <div class="w-1 h-1 bg-blue-400 rounded-full absolute top-7 left-40 "></div>
              <div class="w-1 h-1 bg-yellow-300 rounded-full absolute top-9 left-[20px]"></div>
              <div class="w-1 h-1 bg-red-400 rounded-full absolute top-4 left-[180px]"></div>
              <div class="w-1 h-1 bg-green-300 rounded-full absolute top-8 left-[100px]"></div>
              <div class="w-1 h-1 bg-blue-400 rounded-full absolute top-7 left-[210px]"></div>
              <div class="w-1 h-1 bg-yellow-300 rounded-full absolute top-6 left-[125px]"></div>
              <div class="w-1 h-1 bg-red-400 rounded-full absolute top-7 left-[65px]"></div>
              <div class="w-1 h-1 bg-green-300 rounded-full absolute top-2 left-[220px] "></div>
            </div>
            <!-- Borde ondulado del frosting -->
            <div class="absolute -bottom-3 left-0 right-0 flex">
              <div
                v-for="i in 8"
                :key="i"
                class="flex-1 h-5 bg-[#966969] rounded-b-full"
                :style="{ marginLeft: i > 1 ? '-1px' : '0' }"
              ></div>
            </div>
          </div>
        </div>

        <!-- Velas con números 2 y 0 -->
        <div class="absolute -top-20 left-1/2 transform -translate-x-1/2 flex gap-2">
          <!-- Número 2 -->
          <div class="relative">
            <!-- Vela número 2 solo texto más grande -->
            <div class="relative w-12 h-20 flex items-center justify-center" style="animation: candle-sway 3s ease-in-out infinite;">
              <span class="text-[#e08897] font-black text-6xl drop-shadow-lg" style="text-shadow: 2px 2px 4px rgba(0,0,0,0.3); animation: number-glow 2s ease-in-out infinite;">2</span>
            </div>

            <!-- Llama del número 2 -->
            <div v-if="velasEncendidas[0]" class="absolute -top-1 left-1/2 transform -translate-x-1/2">
              <div class="relative">
                <!-- Resplandor exterior -->
                <div class="absolute inset-0 w-6 h-6 bg-orange-300 rounded-full blur-md opacity-40" style="animation: flame-glow 1.8s ease-in-out infinite;"></div>
                <!-- Resplandor medio -->
                <div class="absolute inset-0 w-4 h-5 bg-yellow-300 rounded-full blur-sm opacity-70" style="animation: flame-glow 1.3s ease-in-out infinite alternate;"></div>
                <!-- Llama principal -->
                <div
                  class="w-3 h-4 bg-gradient-to-t from-orange-600 via-orange-400 to-yellow-300 rounded-full"
                  style="animation: flame-flicker 0.4s ease-in-out infinite alternate, flame-sway 2s ease-in-out infinite;"
                ></div>
              </div>
            </div>

            <!-- Humo del número 2 -->
            <div v-if="!velasEncendidas[0]" class="absolute -top-7 left-1/2 transform -translate-x-1/2">
              <div class="relative">
                <div class="w-1 h-12 bg-gradient-to-t from-gray-500 via-gray-300 to-transparent opacity-60" style="animation: smoke-rise 3.5s ease-out infinite, smoke-drift 4s ease-in-out infinite;"></div>
                <div class="absolute -left-1 top-2 w-0.5 h-10 bg-gradient-to-t from-gray-400 via-gray-200 to-transparent opacity-40" style="animation: smoke-rise 4s ease-out infinite, smoke-drift 4.5s ease-in-out infinite; animation-delay: 0.5s;"></div>
                <div class="absolute left-1 top-1 w-0.5 h-11 bg-gradient-to-t from-gray-500 via-gray-200 to-transparent opacity-50" style="animation: smoke-rise 3.2s ease-out infinite, smoke-drift 3.8s ease-in-out infinite; animation-delay: 1s;"></div>
                <div class="absolute -left-0.5 top-4 w-0.5 h-8 bg-gradient-to-t from-gray-300 to-transparent opacity-30" style="animation: smoke-rise 4.2s ease-out infinite, smoke-drift 5s ease-in-out infinite; animation-delay: 1.5s;"></div>
                <div class="absolute left-0.5 top-3 w-0.5 h-9 bg-gradient-to-t from-gray-400 to-transparent opacity-35" style="animation: smoke-rise 3.6s ease-out infinite, smoke-drift 4.3s ease-in-out infinite; animation-delay: 2s;"></div>
              </div>
            </div>
          </div>

          <!-- Número 0 -->
          <div class="relative">
            <!-- Vela número 0 solo texto más grande -->
            <div class="relative w-12 h-20 flex items-center justify-center" style="animation: candle-sway 3.5s ease-in-out infinite;">
              <span class="text-[#e08897] font-black text-6xl drop-shadow-lg" style="text-shadow: 2px 2px 4px rgba(0,0,0,0.3); animation: number-glow 2.5s ease-in-out infinite;">0</span>
            </div>

            <!-- Llama del número 0 -->
            <div v-if="velasEncendidas[1]" class="absolute -top-1 left-1/2 transform -translate-x-1/2">
              <div class="relative">
                <!-- Resplandor exterior -->
                <div class="absolute inset-0 w-6 h-6 bg-orange-300 rounded-full blur-md opacity-40" style="animation: flame-glow 1.8s ease-in-out infinite;"></div>
                <!-- Resplandor medio -->
                <div class="absolute inset-0 w-4 h-5 bg-yellow-300 rounded-full blur-sm opacity-70" style="animation: flame-glow 1.3s ease-in-out infinite alternate;"></div>
                <!-- Llama principal -->
                <div
                  class="w-3 h-4 bg-gradient-to-t from-orange-600 via-orange-400 to-yellow-300 rounded-full"
                  style="animation: flame-flicker 0.4s ease-in-out infinite alternate, flame-sway 2s ease-in-out infinite;"
                ></div>
              </div>
            </div>

            <!-- Humo del número 0 -->
            <div v-if="!velasEncendidas[1]" class="absolute -top-7 left-1/2 transform -translate-x-1/2">
              <div class="relative">
                <div class="w-1 h-12 bg-gradient-to-t from-gray-500 via-gray-300 to-transparent opacity-60" style="animation: smoke-rise 3.7s ease-out infinite, smoke-drift 4.2s ease-in-out infinite;"></div>
                <div class="absolute -left-1 top-2 w-0.5 h-10 bg-gradient-to-t from-gray-400 via-gray-200 to-transparent opacity-40" style="animation: smoke-rise 4.1s ease-out infinite, smoke-drift 4.7s ease-in-out infinite; animation-delay: 0.5s;"></div>
                <div class="absolute left-1 top-1 w-0.5 h-11 bg-gradient-to-t from-gray-500 via-gray-200 to-transparent opacity-50" style="animation: smoke-rise 3.4s ease-out infinite, smoke-drift 4s ease-in-out infinite; animation-delay: 1s;"></div>
                <div class="absolute -left-0.5 top-4 w-0.5 h-8 bg-gradient-to-t from-gray-300 to-transparent opacity-30" style="animation: smoke-rise 4.4s ease-out infinite, smoke-drift 5.2s ease-in-out infinite; animation-delay: 1.5s;"></div>
                <div class="absolute left-0.5 top-3 w-0.5 h-9 bg-gradient-to-t from-gray-400 to-transparent opacity-35" style="animation: smoke-rise 3.8s ease-out infinite, smoke-drift 4.5s ease-in-out infinite; animation-delay: 2s;"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Globitos decorativos -->
        <!-- Globitos lado izquierdo -->
        <div class="absolute left-4 top-40 ">
          <div v-for="(globo, index) in globosIzquierda" :key="'izq-' + index" 
               :class="['absolute w-16 h-20 rounded-full shadow-lg transition-all duration-1000', globo.color]"
               :style="globo.style">
            <!-- Hilo del globo que va hacia el centro -->
            <div class="absolute top-20 left-1/2 transform -translate-x-1/2 w-0.5 bg-gray-600 opacity-70"
                 :style="globo.hiloStyle"></div>
          </div>
        </div>

        <!-- Globitos lado derecho -->
        <div class="absolute right-4 top-40">
          <div v-for="(globo, index) in globosDerecha" :key="'der-' + index" 
               :class="['absolute w-16 h-20 rounded-full shadow-lg transition-all duration-1000', globo.color]"
               :style="globo.style">
            <!-- Hilo del globo que va hacia el centro -->
            <div class="absolute top-20 left-1/2 transform -translate-x-1/2 w-0.5 bg-gray-600 opacity-70"
                 :style="globo.hiloStyle"></div>
          </div>
        </div>
    </main>

    <!-- Botón abajo -->
    <footer class="pb-12 text-center">
      <button
        class="px-8 py-4 bg-[#185D51] text-white text-xl font-bold rounded-full shadow-lg hover:bg-[#26806f] transition-all duration-300 transform hover:scale-105"
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
      velasEncendidas: [true, true], 
      escuchando: false,
      stream: null,
      globosIzquierda: [
        {
          color: 'bg-red-400',
          style: 'top: -10px; left: 10px; animation: balloon-float 3s ease-in-out infinite;',
          hiloStyle: 'height: 90px; transform-origin: top center; transform: translateX(-50%) rotate(12deg);'
        },
        {
          color: 'bg-blue-400',
          style: 'top: 35px; left: -10px; animation: balloon-float 3.5s ease-in-out infinite; animation-delay: 0.5s;',
          hiloStyle: 'height: 90px; transform-origin: top center; transform: translateX(-50%) rotate(22deg);'
        },
        {
          color: 'bg-yellow-400',
          style: 'top: 70px; left: 8px; animation: balloon-float 4s ease-in-out infinite; animation-delay: 1s;',
          hiloStyle: 'height: 60px; transform-origin: top center; transform: translateX(-50%) rotate(8deg);'
        }
      ],
      globosDerecha: [
        {
          color: 'bg-pink-400',
          style: 'top: -10px; right: 10px; animation: balloon-float 3.2s ease-in-out infinite; animation-delay: 0.2s;',
          hiloStyle: 'height: 90px; transform-origin: top center; transform: translateX(-50%) rotate(-12deg);'
        },
        {
          color: 'bg-green-400',
          style: 'top: 35px; right: -10px; animation: balloon-float 3.8s ease-in-out infinite; animation-delay: 0.7s;',
          hiloStyle: 'height: 90px; transform-origin: top center; transform: translateX(-50%) rotate(-18deg);'
        },
        {
          color: 'bg-purple-400',
          style: 'top: 70px; right: 8px; animation: balloon-float 4.2s ease-in-out infinite; animation-delay: 1.2s;',
          hiloStyle: 'height: 60px; transform-origin: top center; transform: translateX(-50%) rotate(-8deg);'
        }
      ]
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
            this.elevarGlobos();
            this.escuchando = false;
            setTimeout(() => {
              this.$emit('mostrar-carta')
            }, 5000);
            this.stream.getTracks().forEach(t => t.stop());
          }

          if (this.escuchando) requestAnimationFrame(detectarSoplo);
        };

        detectarSoplo();
      } catch (err) {
        alert("No se pudo acceder al micrófono, dame permisos :c");
        console.error(err);
      }
    },
    elevarGlobos() {
      // Animar globos izquierda hacia arriba
      this.globosIzquierda = this.globosIzquierda.map((globo, index) => ({
        ...globo,
        style: `${globo.style} transform: translateY(-300px) translateX(${Math.random() * 40 - 20}px) rotate(${Math.random() * 20 - 10}deg); opacity: 0;`
      }));
      
      // Animar globos derecha hacia arriba
      this.globosDerecha = this.globosDerecha.map((globo, index) => ({
        ...globo,
        style: `${globo.style} transform: translateY(-300px) translateX(${Math.random() * 40 - 20}px) rotate(${Math.random() * 20 - 10}deg); opacity: 0;`
      }));
    }
  }
};
</script>

<style scoped>
@keyframes flame-flicker {
  0% { transform: scale(1) rotate(-2deg); }
  50% { transform: scale(1.15) rotate(2deg); }
  100% { transform: scale(0.9) rotate(-1deg); }
}

@keyframes flame-glow {
  0% { opacity: 0.3; transform: scale(0.9); }
  50% { opacity: 0.8; transform: scale(1.2); }
  100% { opacity: 0.3; transform: scale(0.9); }
}

@keyframes flame-sway {
  0% { transform: translateX(0) rotate(0deg); }
  25% { transform: translateX(2px) rotate(3deg); }
  50% { transform: translateX(0) rotate(0deg); }
  75% { transform: translateX(-2px) rotate(-3deg); }
  100% { transform: translateX(0) rotate(0deg); }
}

@keyframes smoke-drift {
  0% { transform: translateX(0) rotate(0deg); }
  25% { transform: translateX(3px) rotate(5deg); }
  50% { transform: translateX(-2px) rotate(-3deg); }
  75% { transform: translateX(2px) rotate(4deg); }
  100% { transform: translateX(0) rotate(0deg); }
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
    transform: translateY(0) translateX(0) scale(1) rotate(0deg); 
  }
  33% { 
    opacity: 0.5; 
    transform: translateY(-8px) translateX(3px) scale(1.1) rotate(5deg); 
  }
  66% { 
    opacity: 0.3; 
    transform: translateY(-16px) translateX(-2px) scale(1.2) rotate(-3deg); 
  }
  100% { 
    opacity: 0; 
    transform: translateY(-25px) translateX(4px) scale(1.4) rotate(8deg); 
  }
}

@keyframes candle-sway {
  0% { transform: rotate(0deg) scale(1); }
  25% { transform: rotate(1.5deg) scale(1.02); }
  50% { transform: rotate(0deg) scale(1); }
  75% { transform: rotate(-1.5deg) scale(0.98); }
  100% { transform: rotate(0deg) scale(1); }
}

@keyframes number-glow {
  0% { text-shadow: 2px 2px 4px rgba(0,0,0,0.3); }
  50% { text-shadow: 2px 2px 12px rgba(0,0,0,0.5), 0 0 15px currentColor, 0 0 25px currentColor; }
  100% { text-shadow: 2px 2px 4px rgba(0,0,0,0.3); }
}

@keyframes balloon-float {
  0% { transform: translateY(0) rotate(0deg); }
  25% { transform: translateY(-5px) rotate(2deg); }
  50% { transform: translateY(0) rotate(0deg); }
  75% { transform: translateY(-3px) rotate(-2deg); }
  100% { transform: translateY(0) rotate(0deg); }
}
</style>
