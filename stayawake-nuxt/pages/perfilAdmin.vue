<template>
  <div class="form">
    <Nav class="navi" />

    <div class="perfil">
      <Perfil class="formulario" />
    </div>

    <div class="aprobarUsuarios">
      <Aprobar class="cuadroAprobar" />
    </div>

    <div class="asignarruta">
      <AsignarRuta class="cuadroAsignar" />
    </div>

    <div class="crearNotificacion">
      <CrearNoti class="cuadroNotificacion" />
    </div>
  </div>
</template>

<script>
import Nav from '/components/Nav.vue'
import Perfil from '/components/formperfil.vue'
import Aprobar from '/components/UsuariosPendientes.vue'
import AsignarRuta from '/components/rutasAsignadas.vue'
import CrearNoti from '/components/gestionarNoti.vue'
export default {
  components: {
    Nav,
    Perfil,
    Aprobar,
    AsignarRuta,
    CrearNoti,
  },
}
</script>

<style>
/* Perfil del usuario */

.perfil {
  background: url('@/static/img/greenbackground.png');
  height: 100vh;
  padding-top: 5vh;
}

.formulario {
  text-align: center;
  width: 50%;
  margin-left: 25%;
}

.formulario h1 {
  color: black;
}

/* Aprobar Usuarios */

.aprobarUsuarios {
  background: url('@/static/img/bluebackground.png');
  height: 100vh;
}

.cuadroAprobar {
  width: 80%;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Asignacino de rutas */

.asignarruta {
  height: 100vh;
  background: url('@/static/img/greenbackground.png');
  height: 100vh;
  padding-top: 5vh;
}

.cuadroAsignar {
  width: 60%;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Crear notifiaciones */
.crearNotificacion {
  background: url('@/static/img/bluebackground.png');
  height: 100vh;
  padding-top: 4vh;
}

.cuadroNotificacion {
  width: 60%;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.navi {
  height: 8vh;
}
</style>