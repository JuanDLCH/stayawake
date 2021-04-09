<template>
  <div class="form">
    <Nav />

    <div class="perfil">
      <Perfil class="formulario" />
    </div>

    <div class="verruta">
      <Rutas class="rutitas" />
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

.perfil{
  margin: 0;
  width: 60%;
  margin-left: 20%;
  margin-top: 5%;
  height: 100vh;
}
.form {
  /*background-color: rgba(60, 145, 49, 0.411);*/
  background: url('@/static/img/greenbackground.png');
  margin: 0;
}

.formulario h1 {
  color: black;
}

.rutitas {
  height: 100vh;
  width: 60%;
}
</style>