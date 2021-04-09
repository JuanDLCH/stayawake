<template>
  <div class="formularioAprobar">
    <v-card elevation="2" outlined shaped tile class="tarjetaAprobar">
      <h1>Aprobar usuario</h1>
      <v-form ref="formApprove" v-model="valid" lazy-validation id="miform">
        <v-text-field
          v-model="user.id"
          :rules="rules.required"
          label="Identificación"
          :append-icon="'mdi-card-account-details'"
        ></v-text-field>

        <v-btn color="success" @click="searchUser()">Consultar</v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
var findUser
const url_api = 'http://localhost:3001/usuarios/'
export default {
  components: {},

  data: () => ({
    value: String,
    valid: true,

    user: {
      id: '',
      name: '',
      pending: true,
    },

    rules: {
      required: [(v) => !!v || 'El campo es obligatorio'],
    },

    beforeMount() {},
  }),

  methods: {
    async searchUser() {
      try {
        if (this.$refs.formApprove.validate()) {
          //llamado a la api
          let response = await this.$axios.get(url_api)
          let users = response.data
          findUser = users.find((x) => {
            return x.id === this.user.id
          })
          if (findUser) {
            if (findUser.pending) {
              this.$swal
                .fire({
                  type: 'success',
                  title: '¡Usuario encontrado!',
                  text:
                    'ID: ' +
                    findUser.id +
                    ' | | Nombre: ' +
                    findUser.name +
                    ' ' +
                    findUser.lastName,
                  allowEscapeKey: false,
                  allowOutsideClick: false,
                  showCancelButton: true,
                  confirmButtonText: 'Aprobar',
                  cancelButtonText: 'Cancelar'
                })
                .then(async (result) => {
                  if (result.value) {
                    this.updateuser()
                  }
                })
            } else {
              this.$swal.fire({
                type: 'warning',
                title: 'Oops...',
                text: 'El usuario ya está aprobado',
                allowEscapeKey: false,
                allowOutsideClick: false,
              })
              this.$refs.formApprove.reset()
            }
          } else {
            this.$swal.fire({
              type: 'error',
              title: 'Oops...',
              text: 'El usuario no existe o no se ha encontrado',
              allowEscapeKey: false,
              allowOutsideClick: false,
            })
            this.$refs.formApprove.reset()
          }
        }
      } catch (error) {
        console.log(error)
        this.$swal.fire({
          type: 'error',
          title: 'Error al buscar el usuario.',
          text: '',
        })
        this.$refs.formApprove.reset()
      }
    },

    async updateuser() {
      if (this.$refs.formApprove.validate()) {
        // Crear un nuevo objeto con la info del usuario
        findUser.pending = false
        let user = Object.assign({}, findUser)
        let response = await this.$axios.put(
          'http://localhost:3001/usuarios/' + user.id,
          user
        )

        console.log(user.pending)
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
.formularioAprobar {
  width: 40%;
  text-align: center;
  margin: 0;
  height: 23%;
}

.formularioAprobar h1 {
  color: black;
}

.tarjetaAprobar {
  padding: 5%;
  padding-left: 10%;
  padding-right: 10%;
  width: 100%;
}
</style>