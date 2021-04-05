<template>
  <div class="login">
    <div class="loginitems">
      <h1>Inicia Sesion</h1>

      <v-form ref="formLogin" v-model="valid" lazy-validation id="form">
        <v-text-field
          id="txtUser"
          class="cajatexto"
          v-model="user.id"
          :rules="idRules"
          label="Identificación"
          :append-icon="'mdi-card-account-details'"
        ></v-text-field>

        <v-text-field
          class="cajatexto"
          label="Contraseña"
          v-model="user.password"
          :rules="fieldrules"
          :append-icon="value ? 'mdi-eye-off' : 'mdi-eye'"
          @click:append="() => (value = !value)"
          :type="value ? 'password' : 'text'"
        >
        </v-text-field>

        <v-btn class="boton" color="success" @click="login()">Ingresar</v-btn>
      </v-form>

      <a class="subraya" @click="enproceso">¿Olvidaste tu contraseña?</a>

      <p>¿No tienes cuenta? <a href="/register">Registrate</a></p>
    </div>
  </div>
</template>

<script>
const url_api = 'http://localhost:3001/usuarios/'

export default {
  data: () => ({
    value: String,
    valid: true,
    user: {},
    fieldrules: [(v) => !!v || 'La clave es obligatoria'],
    idRules: [(v) => !!v || 'La identificación es obligatoria'],
  }),

  methods: {
    enproceso() {
      this.$swal.fire({
        type: 'warning',
        title: 'Sección en construcción',
        text: '',
      })
    },

    async login() {
      try {
        if (this.$refs.formLogin.validate()) {
          //llamado a la api
          let response = await this.$axios.get(url_api)
          let users = response.data
          let findUser = users.find((x) => {
            return x.id === this.user.id && x.password === this.user.password
          })
          if (findUser) {
            delete findUser.password
            localStorage.setItem('user-in', findUser.id)

            this.$swal.fire({
              type: 'success',
              title: 'Exito',
              text: 'Inicio de sesion exitoso',
              allowEscapeKey: false,
              allowOutsideClick: false,
            })

            this.$router.push('/perfil')
          } else {
            this.$swal.fire({
              type: 'error',
              title: 'Oops...',
              text: 'El correo o la contraseña son incorrectos.',
              allowEscapeKey: false,
              allowOutsideClick: false,
            })
            this.$refs.formLogin.reset()
          }
        }
      } catch (error) {
        console.log(error)
        this.$swal.fire({
          type: 'error',
          title: 'Error al iniciar sesión.',
          text: '',
        })
        this.$refs.formLogin.reset()
      }
    },
  },
}
</script>

<style>
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

.v-input__slot{
  background-color: white;
  padding: 10px;
}

.button span {
  margin-bottom: 20px;
  width: 40%;
}

.subraya {
  cursor: pointer;
  text-decoration: underline white;
}
</style>