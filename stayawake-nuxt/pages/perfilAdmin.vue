<template>
  <div class="form">
    <Nav class="navi" />

    <div class="contenedors">
      <Perfil class="formulario" />

      <div class="contenedor-secundarios">
          <Aprobar class="cuadroAprobar"/>
          <AsignarRuta class="cuadroAsignar" />
      </div>
    </div>
  </div>
</template>

<script>
import Nav from '/components/Nav.vue'
import Perfil from '/components/formperfil.vue'
import Aprobar from '/components/AprobarUsuario.vue'
import AsignarRuta from '/components/AsignarRuta.vue'
export default {
  components: {
    Nav,
    Perfil,
    Aprobar,
    AsignarRuta,
  },
}
</script>

<style>
.formulario {
    padding-top: 12vh;
  margin-left: 10%;
  text-align: center;
}

.contenedors{
    align-self: center;
    width: 80%;
    margin-left: 10%;
    padding-top: 0;
    display: flex;


}

.contenedor-secundarios{
    padding-top: 8vh;
    float: right;
    margin-left: 10%;
    width: 40%;
}

.cuadroAprobar{
    margin-top: 4%;
    width: 100%;
}

.cuadroAsignar{
    margin: 0;
    margin-top: 10%;
}

.cuadroAsignar div{
    margin: 0;
}

.navi{
    height: 8vh;
}
</style>