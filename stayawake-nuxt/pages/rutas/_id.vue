<template>
  <div class="formularioAnadir">
    <v-card elevation="2" outlined shaped tile class="tarjetaAnadir">
      <h1>Asignar Rutas</h1>
      <v-form ref="formAnadir" v-model="valid" lazy-validation id="miform">
        <v-text-field
          v-model="route.idConductor"
          :rules="rules.required"
          label="ID del conductor a asignar"
          :append-icon="'mdi-card-account-details'"
        ></v-text-field>

        <v-text-field
          v-model="route.fecha"
          :rules="rules.required"
          label="Fecha de inicio de ruta"
          :append-icon="'mdi-calendar'"
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
          :append-icon="'mdi-message-reply-text'"
        ></v-textarea>

        <v-select
          v-model="route.estado"
          :rules="rules.required"
          :items="categories"
          label="Estado de la ruta"
          required
        ></v-select>

        <v-btn color="success" @click="searchUser()">Actualizar</v-btn>
        <v-btn color="error" to="../perfilAdmin">Volver</v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
var findUser
const url_api = 'http://localhost:3001/rutas/'
export default {
  async asyncData({ params }) {
    let id = params.id
    return { id }
  },
  components: {},

  data: () => ({
    value: String,
    valid: true,

    route: {},

    categories: ['No iniciada', 'En curso', 'Completada'],

    rules: {
      required: [(v) => !!v || 'El campo es obligatorio'],
    },
  }),

  beforeMount() {
    this.getRoute()
  },

  methods: {
    async getRoute() {
      try {
        let response = await this.$axios.get(url_api + this.id)
        this.route = response.data
      } catch (error) {
        console.error(error)
      }
    },

    async searchUser() {
      try {
        if (this.$refs.formAnadir.validate()) {
          //llamado a la api
          let response = await this.$axios.get('http://localhost:3001/usuarios/')
          let users = response.data
          findUser = users.find((x) => {
            return x.id === this.route.idConductor
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
                this.updateroute()
              }
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
          text: error,
        })
        this.$refs.formAnadir.reset()
      }
    },

    async updateroute() {
      if (this.$refs.formAnadir.validate()) {
        // Crear un nuevo objeto con la info del usuario
        let route = Object.assign({}, this.route)
        let response = await this.$axios.put(
          'http://localhost:3001/rutas/' + route.id,
          route
        )
        this.$swal.fire({
          type: 'success',
          title: 'Operación exitosa.',
          text: 'El item se actualizo correctamente.',
        })
        this.$refs.formAnadir.reset()
      } else {
        this.$swal.fire({
          type: 'warning',
          title: 'Formulario incompleto.',
          text: 'Hay campos que deben ser diligenciados. xd',
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