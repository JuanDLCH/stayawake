<template>
  <div class="formularioAnadir">
    <v-card elevation="2" outlined shaped tile class="tarjetaAnadir">
      <h1>Asignar Ruta</h1>
      <v-form ref="formAnadir" v-model="valid" lazy-validation id="miform">
        <v-text-field
          v-model="route.id"
          :rules="rules.required"
          label="ID del conductor a asignar"
          :append-icon="'mdi-card-account-details'"
        ></v-text-field>

        <v-text-field
          v-model="route.salida"
          :rules="rules.required"
          label="Punto de inicio"
          :append-icon="'mdi-map-marker'"
        ></v-text-field>

        <v-text-field
          v-model="route.llegada"
          :rules="rules.required"
          label="Punto de llegada"
          :append-icon="'mdi-map-marker-radius'"
        ></v-text-field>

        <v-textarea
          v-model="route.observation"
          label="Observaciones"
        ></v-textarea>

        <v-btn color="success" @click="searchUser()">Asignar</v-btn>
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

    route: {
      id: '',
      salida: '',
      llegada: '',
    },

    rules: {
      required: [(v) => !!v || 'El campo es obligatorio'],
    },

    beforeMount() {},
  }),

  methods: {
    async searchUser() {
      try {
        if (this.$refs.formAnadir.validate()) {
          //llamado a la api
          let response = await this.$axios.get(url_api)
          let users = response.data
          findUser = users.find((x) => {
            return x.id === this.route.id
          })
          if (findUser) {
            if (findUser.pending) {
              this.$swal.fire({
                type: 'warning',
                title: 'Error',
                text:
                  'El usuario no ha sido aprobado, apruebe su registro antes de asignarle una ruta',
                allowEscapeKey: false,
                allowOutsideClick: false,
              })
            } else {
              if (findUser.category === 'Administrador') {
                this.$swal.fire({
                  type: 'warning',
                  title: 'Error',
                  text: 'El usuario no está registrado como un conductor',
                  allowEscapeKey: false,
                  allowOutsideClick: false,
                })
              } else {
                  this.setRoute()
              }
              this.$refs.formAnadir.reset()
            }
          } else {
            this.$swal.fire({
              type: 'error',
              title: 'Oops...',
              text: 'El usuario no existe o no se ha encontrado',
              allowEscapeKey: false,
              allowOutsideClick: false,
            })
            this.$refs.formAnadir.reset()
          }
        }
      } catch (error) {
        console.log(error)
        this.$swal.fire({
          type: 'error',
          title: 'Error al buscar el usuario.',
          text: '',
        })
        this.$refs.formAnadir.reset()
      }
    },

    async setRoute() {
      if (this.$refs.formAnadir.validate()) {
        let route = Object.assign({}, this.route)
        console.log(route)

        try {
          let response = await this.$axios.post(
            'http://localhost:3001/rutas',
            route
          )
          console.log(response)
          this.$swal.fire({
            type: 'success',
            title: 'Exito',
            text: 'Se agrego la ruta correctamente',
          })
        } catch (error) {
          this.$swal.fire({
            type: 'warning',
            title: 'ERROR',
            text: 'Este usuario ya tiene asignada una ruta, no se podra asignar otra hasta que no la marque como completada',
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
      this.$refs.formAnadir.reset()
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
.formularioAnadir {
  width: 100%;
  text-align: center;
  margin: 0;
}

.formularioAnadir h1 {
  color: black;
}

.tarjetaAnadir {
  padding: 5%;
  padding-left: 10%;
  padding-right: 10%;
  width: 100%;
}
</style>