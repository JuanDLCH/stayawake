<template>
  <div class="formularioNotif">
    <v-card elevation="2" outlined shaped tile class="tarjetaNotif">
      <h1>Editar Notificacion</h1>
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

        <v-btn color="success" @click="updatenotification()">Actualizar</v-btn>
        <v-btn color="error" to="../perfilAdmin">Volver</v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
var findUser
var idtodelete
const url_api = 'http://localhost:3001/recordatorios/'
export default {
  async asyncData({ params }) {
    let id = params.id
    return { id }
  },

  components: {},

  data() {
    return {
      value: String,
      valid: true,

      notification: {},

      rules: {
        required: [(v) => !!v || 'El campo es obligatorio'],
      },
    }
  },

  beforeMount() {
    this.getNotification()
  },

  methods: {
    async getNotification() {
      try {
        let response = await this.$axios.get(url_api + this.id)
        this.notification = response.data
      } catch (error) {
        console.error(error)
      }
    },

    async updatenotification() {
      try {
        // Crear un nuevo objeto con la info del usuario
        let notification = Object.assign({}, this.notification)
        let response = await this.$axios.put(url_api + this.id, notification)
        this.$swal.fire({
          type: 'success',
          title: 'Operación exitosa.',
          text: 'El item se actualizo correctamente.',
        })
        this.$router.push('perfilAdmin')
      } catch (error) {
        this.$swal.fire({
          type: 'error',
          title: 'Error.',
          text: 'Ocurrio un error al actualizar.',
        })
      }
    },
  },
}
</script>