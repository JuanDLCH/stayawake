<template>
  <div class="form">
    <Nav />

    <div class="contenedor">
      <Perfil class="formulario" />

      <div class="contenedor-secundario">
        <Rutas class="rutitas" />
      </div>
    </div>
  </div>
</template>

<script>
import Nav from '/components/Nav.vue'
import Perfil from '/components/formperfil.vue'
import Rutas from '/components/Rutas'

export default {
  components: {
    Nav,
    Perfil,
    Rutas,
  },

  data() {
    return {}
  },
}
</script>

<style>
.formulario {
  margin-top: 5%;
  width: 40%;
}

.contenedor {
  width: 80%;
}

.contenedor-secundario{
  margin-top: 5%;
  width: 40%;
}

.rutitas {
  margin-top: 10%;
}
</style>