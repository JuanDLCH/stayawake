<template>
  <div class="gestionarNoti">
    <v-card>
      <v-card-actions>
        <h1 class="acheuno">Gestionar Notificaciones</h1>
        <v-spacer></v-spacer>
        <v-btn color="success" to="notis">Crear Notificacion</v-btn>
      </v-card-actions>

      <v-card-text>
        <v-data-table
          :headers="headers"
          :items="notifications"
          :items-per-page="5"
          class="elevation-1"
        >
          <template v-slot:item.actions="{ item }">
            <v-icon class="mr-2" @click="showNoti(item)"> mdi-eye </v-icon>
            <v-icon class="mr-2" @click="editnotification(item)">
              mdi-pencil
            </v-icon>
            <v-icon @click="deletenotification(item)"> mdi-delete </v-icon>
          </template>
        </v-data-table>
      </v-card-text>
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
      headers: [
        {
          text: 'ID',
          align: 'start',
          sortable: true,
          value: 'id',
        },
        { text: 'Titulo', value: 'title' },
        { text: 'Mensaje', value: 'msg' },
        { text: 'Acciones', value: 'actions' },
      ],
      notifications: [],

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

  beforeMount() {
    this.getNotifications()
  },

  methods: {
    async getNotifications() {
      try {
        let response = await this.$axios.get(url_api)
        this.notifications = response.data
      } catch (error) {
        console.error(error)
      }
    },

    async editnotification(item) {
      this.$router.push('notis/'+ item.id)
    },

    async askforid() {
      if (this.$refs.formNotif.validate()) {
        this.$swal
          .fire({
            title: 'Ingrese el ID de la notifiacion a actualizar',
            input: 'number',
            inputAttributes: {
              autocapitalize: 'off',
            },
            showCancelButton: true,
            confirmButtonText: 'Actualizar',
            showLoaderOnConfirm: true,
            preConfirm: (id) => {
              this.idtodelete = id
              this.updatenotification(id)
            },
            allowOutsideClick: () => !Swal.isLoading(),
          })
          .then((result) => {
            if (result.isConfirmed) {
              Swal.fire({
                title: `${result.value.login}'s avatar`,
                imageUrl: result.value.avatar_url,
              })
            }
          })
      } else {
        this.$swal.fire({
          type: 'warning',
          title: 'Formulario incompleto.',
          text: 'Hay campos que deben ser diligenciados',
        })
      }
    },

    async updatenotification(id) {
      try {
        // Crear un nuevo objeto con la info del usuario
        let notification = Object.assign({}, this.notification)
        let response = await this.$axios.put(
          'http://localhost:3001/recordatorios/' + id,
          notification
        )
        this.$swal.fire({
          type: 'success',
          title: 'Operación exitosa.',
          text: 'El item se actualizo correctamente.',
        })
        this.$refs.formNotif.reset()
      } catch (error) {
        this.$swal.fire({
          type: 'error',
          title: 'Error.',
          text: 'No existe una notificacion con este id.',
        })
      }
    },

    deletenotification(item) {
      this.$swal
        .fire({
          type: 'warning',
          title: '¿Está seguro de eliminar una notificacion?',
          text: 'Ningún dato asociado a ella podrá recuperarse.',
          allowEscapeKey: false,
          allowOutsideClick: false,
          showCancelButton: true,
        })
        .then(async (result) => {
          if (result.value) {
            try {
              let url = url_api + item.id
              await this.$axios.delete(url)
              this.$swal.fire({
                type: 'success',
                title: 'Operación exitosa.',
                text: 'La notificación se eliminó correctamente.',
              })
              this.getNotifications()
            } catch (error) {
              this.$swal.fire({
                type: 'error',
                title: 'Error',
                text: 'No se encontró esta notificación',
              })
            }
          }
        })
    },

    async showNoti(item) {
      try {
        //
        let response = await this.$axios.get(url_api + item.id)
        this.noti = response.data
        this.$swal.fire({
          title: this.noti.title,
          text: this.noti.msg,
        })
      } catch (error) {
        this.$swal
          .fire({
            type: 'error',
            title: 'Oops...',
            text: 'La notificacion no existe o hubo un error cargandola.',
            allowEscapeKey: false,
            allowOutsideClick: false,
          })
          .then((result) => {
            if (result.value) {
            }
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
.gestionarNoti {
  width: 100%;
}
.formularioNotif {
  width: 100%;
  text-align: center;
  margin: 0;
}

.formularioNotif h1 {
  color: black;
}

.tarjetaNotif {
  padding: 5%;
  padding-left: 10%;
  padding-right: 10%;
  width: 100%;
}
</style>