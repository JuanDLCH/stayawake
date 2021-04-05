<template>
  <!-- Encabezado -->
  <header>
    <!-- Menu de navegacion -->
    <div class="navegacion">
      <Nav />

      <div class="principal">
        <div class="textocentrado">
          <h1>StayAwake</h1>
          <p>
            Protegemos tu vida y la de los demás actores viales en la carretera,
            creamos consciencia en la via y salvamos la vida de muchos
            conductoresy pasajeros de ser victimas de accidentes por
            microsueños.
          </p>
          <p>¡Mantente despierto!</p>
          <p>Tu familia te espera.</p>
        </div>
      </div>

      <Login />
    </div>
  </header>
</template>

<script>
import Nav from '/components/Nav.vue'
import Login from '/components/Login.vue'
export default {
    components: {
    Login, Nav
  },
}
</script>


<style>
.boton {
  margin: 10px;
}
.boton span {
  color: black;
}

/* General */

body {
  margin: 0;
  padding: 0;
  background: black;
}

h1 {
  color: white;
}

a {
  color: white;
}

p {
  color: white;
}

label {
  color: white;
}

h2 {
  color: white;
}



/* Imagen de inicio */

.navegacion {
  height: 100vh;
  width: 100%;
  background: url('@/static/img/camionmontanas.jpg');
  background-size: 100% 100%;
  position: absolute;
  display: flex;
}

/* Texto inicio */

.principal {
  z-index: 1;
  width: 70%;
  height: 100vh;
  float: left;
  text-align: center;
  position: relative;
  background: rgba(0, 0, 0, 0.452);
}

.textocentrado {
  color: white;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  width: 60%;
}

.textocentrado h1 {
  margin-top: 0;
  font-size: 50px;
  margin-bottom: 0;
}

.textocentrado p {
  font-size: 20px;
  margin-top: 10px;
  color: rgb(255, 255, 255);
}
</style>