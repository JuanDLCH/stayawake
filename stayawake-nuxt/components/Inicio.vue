<template>
    <!-- Encabezado -->
    <header>
      <!-- Menu de navegacion -->
      <div class="navegacion">
        <nav>
          <nuxt-link to="/"
            ><img src="@/static/img/stayawakelogo.svg" alt="logo" class="logo"
          /></nuxt-link>
          <ul>
            <li><nuxt-link to="/">Inicio</nuxt-link></li>
            <li><nuxt-link to="/#origen">Origen</nuxt-link></li>
            <li><nuxt-link to="/#objetivo">Objetivo</nuxt-link></li>
            <li><nuxt-link to="/#nosotros">Nosotros</nuxt-link></li>
            <li>
              <nuxt-link to="/#contactanos">Contactanos</nuxt-link>
            </li>
          </ul>
        </nav>

        <div class="principal">
          <div class="textocentrado">
            <h1>StayAwake</h1>
            <p>
              Protegemos tu vida y la de los demás actores viales en la
              carretera, creamos consciencia en la via y salvamos la vida de
              muchos conductoresy pasajeros de ser victimas de accidentes por
              microsueños.
            </p>
            <p>¡Mantente despierto!</p>
            <p>Tu familia te espera.</p>
          </div>
        </div>

        <div class="login">
          <div class="loginitems">
            <h1>Inicia Sesion</h1>

            <v-form ref="formRegister" v-model="valid" lazy-validation id="form">
              <v-text-field
               class="cajatexto"
                v-model="product.id"
                :rules="rules.required"
                label="Identificación"
              ></v-text-field>

              <v-text-field 
              class="cajatexto"
              label="Contraseña" 
              v-model="product.password"
              :rules="rules.required"
              type="password">
              </v-text-field>

              <v-btn class="boton" color="success" @click="validarlogin()">Ingresar</v-btn>
            </v-form>

            <a href="">¿Olvidaste tu contraseña?</a>

            <p>¿No tienes cuenta? <a href="/register">Registrate</a></p>
          </div>
        </div>
      </div>
    </header>

</template>

<script>
export default {

  data: () => ({
    valid: true,
    product: {
      id: '',
      name: '',
    },
    rules: {
      required: [(v) => !!v || 'El campo es obligatorio'],
    },
  }),

  methods: {
    async validarlogin() {
      if (this.$refs.formRegister.validate()) {
        let product = Object.assign({}, this.product)
        console.log(product)

        //json-server --watch db.json -p 3001

        let response = await this.$axios.post(
          'http://localhost:3001/usuarios',
          product
        )
        console.log(response)
      } else {
        console.log('Formualario incompleto')
      }
    },
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    },
  },
}
</script>


<style>

.boton{
    margin: 10px;
}
.boton span{
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

/* Barra de navegacion */
header {
  height: 100vh;
  width: 100%;
  position: relative;
}

.logo {
  height: 90%;
  width: 10%;
  margin: 5px;
}

nav {
  align-items: center;
  content: '';
  position: fixed;
  height: 10vh;
  bottom: 0;
  right: 0;
  left: 0;
  top: 0;
  background: rgba(0, 0, 0, 0.65);
  z-index: 4;
}
nav ul {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;
  align-items: center;
  list-style-type: none;
  margin-top: 0;
  height: 5vh;
}

nav li {
  margin: 7px;
}

nav a {
  color: white;
  text-decoration: none;
  font-size: 20px;
}

nav a:hover {
  font-size: 23px;
  color: rgb(184, 184, 184);
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

/* Login */

.login {
  z-index: 3;
  width: 30%;
  height: 100vh;
  float: right;
  text-align: center;
  position: relative;
  background: rgba(0, 43, 68, 0.849);
  box-shadow: -21px -1px 3px rgba(0, 0, 0, 0.356);
}

.loginitems {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.textbox {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.textbox input {
  width: 250px;
  margin-bottom: 20px;
}

.button input {
  margin-bottom: 20px;
  width: 40%;
}
</style>