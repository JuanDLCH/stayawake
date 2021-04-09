<template>
    <v-card elevation="2" outlined shaped tile class="tarjeta">
      <h1>Perfil de Usuario</h1>
      <v-form ref="formUpdate" v-model="valid" lazy-validation id="miform">
        <v-text-field
          v-model="user.id"
          :rules="rules.required"
          label="Identificación"
          :readonly="true"
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

        <v-text-field
          v-model="user.category"
          :rules="rules.required"
          label="Tipo"
          :readonly="true"
          :append-icon="'mdi-account-key'"
        ></v-text-field>

        <v-btn color="success" @click="updateuser()">Actualizar</v-btn>

        <v-btn color="error" @click="deleteuser()">Eliminar Usuario</v-btn>
      </v-form>
    </v-card>
</template>

<script>
export default {
  components: {},

  data: () => ({
    value: String,
    valid: true,
    user: {
      id: '',
      name: '',
    },
    rules: {
      required: [(v) => !!v || 'El campo es obligatorio'],
    },

    email: '',
    emailRules: [
      (v) => !!v || 'E-mail requerido',
      (v) => /.+@.+\..+/.test(v) || 'E-mail inválido',
    ],
  }),

  beforeMount() {
    this.getuser(localStorage.getItem('user-in'))
  },

  methods: {
    async getuser(usuario) {
      try {
        //
        let response = await this.$axios.get(
          'http://localhost:3001/usuarios/' + usuario
        )
        this.user = response.data
      } catch (error) {
        this.$swal
          .fire({
            type: 'error',
            title: 'Oops...',
            text: 'El usuario no existe o hubo un error cargandolo.',
            allowEscapeKey: false,
            allowOutsideClick: false,
          })
          .then((result) => {
            if (result.value) {
              this.$router.push('/')
            }
          })
      }
    },
    /**
     * Enviar una solicitud (Request) en un método update
     * Para modificar el usero
     */
    async updateuser() {
      if (this.$refs.formUpdate.validate()) {
        // Crear un nuevo objeto con la info del usuario
        let user = Object.assign({}, this.user)
        let response = await this.$axios.put(
          'http://localhost:3001/usuarios/' + user.id,
          user
        )
        this.$swal.fire({
          type: 'success',
          title: 'Operación exitosa.',
          text: 'El item se actualizo correctamente.',
        })
      } else {
        this.$swal.fire({
          type: 'warning',
          title: 'Formulario incompleto.',
          text: 'Hay campos que deben ser diligenciados.',
        })
      }
    },

    deleteuser() {
      this.$swal
        .fire({
          type: 'warning',
          title: '¿Está seguro de eliminar el usuario?',
          text: 'Ningún dato asociado a él podrá recuperarse.',
          allowEscapeKey: false,
          allowOutsideClick: false,
          showCancelButton: true,
        })
        .then(async (result) => {
          if (result.value) {
            try {
              let url = 'http://localhost:3001/usuarios/' + this.user.id
              await this.$axios.delete(url)
              this.$swal.fire({
                type: 'success',
                title: 'Operación exitosa.',
                text: 'El item se eliminó correctamente.',
              })
              this.$router.push('/')
            } catch (error) {
              this.$swal.fire({
                type: 'error',
                title: 'Ha ocurrido un problema al eliminar',
                text: error.toString(),
              })
            }
          }
        })
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
  padding: 5%;
  padding-top: 2%;
  padding-bottom: 2%;
}

.v-input__slot {
  background-color: white;
}
</style>