<template>
  <div class="form">
    <Nav />
    <div class="formulario">
      <v-card elevation="2" outlined shaped tile class="tarjeta">
        <h1>Registro</h1>
        <v-form ref="formRegister" v-model="valid" lazy-validation id="miform">
          <v-text-field
            v-model="user.id"
            :rules="rules.required"
            label="Identificación"
            :append-icon="'mdi-card-account-details'"
          ></v-text-field>

          <v-text-field
            v-model="user.name"
            :rules="rules.required"
            label="Nombre"
            required
            :append-icon="'mdi-account-box'"
          ></v-text-field>

          <v-text-field
            v-model="user.lastName"
            :rules="rules.required"
            label="Apellidos"
            required
            :append-icon="'mdi-account-box'"
          ></v-text-field>

          <v-text-field
            v-model="user.email"
            :rules="emailRules"
            label="E-mail"
            required
            :append-icon="'mdi-email'"
          ></v-text-field>

          <v-text-field
            v-model="user.password"
            :rules="rules.required"
            label="Contraseña"
            required
            :append-icon="value ? 'mdi-eye-off' : 'mdi-eye'"
            @click:append="() => (value = !value)"
            :type="value ? 'password' : 'text'"
          ></v-text-field>

          <v-select
            v-model="user.category"
            :rules="rules.required"
            :items="categories"
            label="¿Cómo vas a usar la aplicación?"
            required
          ></v-select>

          <v-btn color="success" @click="saveUser()"
            >Registrarse</v-btn
          >
        </v-form>
      </v-card>
    </div>
  </div>
</template>

<script>
import Nav from '/components/Nav.vue'
export default {
  components: {
    Nav,
  },

  data: () => ({
    value: String,
    valid: true,

    user: {
      id: '',
      name: '',
      pending: true,
    },

    categories: ['Administrador', 'Conductor'],

    rules: {
      required: [(v) => !!v || 'El campo es obligatorio'],
    },

    beforeMount() {},

    email: '',
    emailRules: [
      (v) => !!v || 'E-mail requerido',
      (v) => /.+@.+\..+/.test(v) || 'E-mail inválido',
    ],
  }),

  beforeMount() {},

  methods: {
    async saveUser() {
      if (this.$refs.formRegister.validate()) {
        let user = Object.assign({}, this.user)
        console.log(user)

        //json-server --watch db.json -p 3001
        try {
          let response = await this.$axios.post(
            'http://localhost:3001/usuarios',
            user
          )
          console.log(response)
          this.$swal.fire({
            type: 'success',
            title: 'Formulario diligenciado correctamente.',
            text: 'El registro se realizó',
          })
        } catch (error) {
          this.$swal.fire({
            type: 'warning',
            title: 'ERROR',
            text: 'El usuario ya existe',
          })
        }
      } else {
        console.log('Formualario incompleto')
        this.$swal.fire({
          type: 'warning',
          title: 'Formulario incompleto.',
          text: 'Todos los campos deben ser diligenciados',
        })
      }
      this.$refs.formRegister.reset()
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
.tarjeta {
  padding: 10%;
  margin-top: 10vh;
}
.formulario {
  width: 40%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  margin: 0;
  margin-top: 5vh;
}
form {
  margin: 0;
  width: 100%;
}

.formulario h1 {
  color: black;
}
.form {
  height: 100vh;
  /*background-color: rgba(0, 35, 230, 0.411);*/
  background: url('@/static/img/bluebackground.png');
  background-size: 100% 100%;
  margin: 0;
}

.button span {
  color: black;
  margin: 0;
}
</style>