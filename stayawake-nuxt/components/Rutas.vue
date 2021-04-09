<template>
  <div class="formularioRutas">
    <v-card elevation="2" outlined shaped tile class="tarjetaRutas">
      <h1>Rutas Asignadas</h1>
      <v-form ref="formRutas" v-model="valid" lazy-validation id="miform">
        <v-text-field
          v-model="route.salida"
          :rules="rules.required"
          label="Punto de inicio"
          :readonly="true"
          :append-icon="'mdi-map-marker'"
        ></v-text-field>

        <v-text-field
          v-model="route.llegada"
          :rules="rules.required"
          label="Punto de llegada"
          :append-icon="'mdi-map-marker-radius'"
          :readonly="true"
        ></v-text-field>

        <v-textarea
          v-model="route.observation"
          label="Observaciones"
          :readonly="true"
          :append-icon="'mdi-message-reply-text'"
        ></v-textarea>

        <v-btn color="success" @click="completar()"> Completada </v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
export default {
  components: {},

  data: () => ({
    value: String,
    valid: true,
    route: {
      salida: 'No asignada',
      llegada: 'No asignada',
      observation: 'No se le ha asignado ninguna ruta todavia',
    },
    rules: {
      required: [(v) => !!v || 'El campo es obligatorio'],
    },
  }),

  beforeMount() {
    this.getRoute(localStorage.getItem('user-in'))
  },

  methods: {
    async getRoute(usuario) {
      try {
        //
        let response = await this.$axios.get(
          'http://localhost:3001/rutas/' + usuario
        )
        this.route = response.data
      } catch (error) {
        route.salida.data = 'No asignada'
        route.llegada = 'No asignada'
        route.observation = 'Usted no ha sido asignado a una ruta aun'
      }
    },

    completar() {
      this.$swal
        .fire({
          type: 'warning',
          title: '¿Completaste esta ruta?',
          text:
            'Marcar esta ruta como completa te dejará disponible para ser asignado a otra',
          allowEscapeKey: false,
          allowOutsideClick: false,
          showCancelButton: true,
        })
        .then(async (result) => {
          if (result.value) {
            try {
              let url =
                'http://localhost:3001/rutas/' + localStorage.getItem('user-in')
              await this.$axios.delete(url)
              this.$swal.fire({
                type: 'success',
                title: 'Operación exitosa.',
                text: 'Marcaste la ruta como completada',
              })
              this.$router.push('/')
            } catch (error) {
              this.$swal.fire({
                type: 'error',
                title: 'Ha ocurrido un problema al completar',
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

.formularioRutas {
  width: 100%;
  height: 100vh;
  margin-left: 20%;
  text-align: center;
}

.formularioRutas h1 {
  color: black;
}

.tarjetaRutas {
  padding: 5%;
  padding-left: 10%;
  padding-right: 10%;
  margin-bottom: 10%;
}
</style>