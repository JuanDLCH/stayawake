<template>
  <body>
    <link>

    <!-- Primera pantalla de la pagina -->

    <Inicio />

    <!-- Cuerpo -->
    <main>

      <Origen />

      <Objetivo />

    </main>

    <!-- Footer -->

    
  </body>
</template>

<script>
import Inicio from '/components/Inicio.vue'
import Origen from '/components/Origen.vue'
import Objetivo from '/components/Objetivo.vue'
export default {
  components: {
    Inicio, Origen, Objetivo
  },
}
</script>

<style>


</style>