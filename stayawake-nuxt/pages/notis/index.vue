<template>
  <div class="formularioNotif">
    <v-card elevation="2" outlined shaped tile class="tarjetaNotif">
      <h1>Crear Notifiacion</h1>
      <v-form ref="formNotif" v-model="valid" lazy-validation id="miform">
        <v-text-field
          v-model="notification.title"
          :rules="rules.required"
          label="Title"
          :append-icon="'mdi-card-account-details'"
        ></v-text-field>

        <v-textarea
          v-model="notification.msg"
          label="Mensaje"
          :rules="rules.required"
          :append-icon="'mdi-message-reply-text'"
        ></v-textarea>

        <v-btn color="success" @click="setnotification()">Añadir</v-btn>
        <v-btn color="error" to="perfilAdmin">Volver</v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
var findUser
var idtodelete
const url_api = 'http://localhost:3001/recordatorios/'
export default {
  components: {},

  data() {
    return {
      value: String,
      valid: true,

      notification: {
        id: '',
        title: '',
        msg: '',
      },

      rules: {
        required: [(v) => !!v || 'El campo es obligatorio'],
      },
    }
  },

  methods: {
    async setnotification() {
      if (this.$refs.formNotif.validate()) {
        let notification = Object.assign({}, this.notification)
        console.log(notification)

        try {
          let response = await this.$axios.post(
            'http://localhost:3001/recordatorios',
            notification
          )
          console.log(response)
          this.$swal.fire({
            type: 'success',
            title: 'Exito',
            text:
              'Se agrego la notificacion correctamente'
          })
          this.$router.push('../perfilAdmin') 
        } catch (error) {
          this.$swal.fire({
            type: 'warning',
            title: 'Atencion',
            text: 'Ocurrio un error inesperado',
            allowEscapeKey: false,
            allowOutsideClick: false,
          })
        }
      } else {
        console.log('Formulario incompleto')
        this.$swal.fire({
          type: 'warning',
          title: 'Formulario incompleto.',
          text: 'Todos los campos deben ser diligenciados',
        })
      }
    },
  },
}
</script>