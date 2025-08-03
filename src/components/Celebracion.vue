<template>
  <main class="relative w-full h-screen overflow-hidden">
    <Cake v-if="!mostrarCarta" @mostrar-carta="mostrarCarta = true" />
    <Carta v-else />
  </main>
</template>

<script>
import Cake from './Pastel.vue'
import Carta from './Carta.vue'

export default {
  components: { Cake, Carta},
  data() {
    return {
      mostrarCarta: false
    }
  }
}
</script>
