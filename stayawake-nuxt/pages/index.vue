<template>
  <div>
    <body>
      <!-- Primera pantalla de la pagina -->
      <Inicio />
    </body>

    <main>
      <!-- Cuerpo -->
      <Origen />

      <Objetivo />
    </main>

    <!-- Footer -->
  </div>
</template>

<script>
import Inicio from '/components/Inicio.vue'
import Origen from '/components/Origen.vue'
import Objetivo from '/components/Objetivo.vue'
export default {
  components: {
    Inicio,
    Origen,
    Objetivo,
  },
}
</script>

<style>
</style>