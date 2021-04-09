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

        <v-btn color="success" @click="setnotification()">Crear</v-btn>
        <v-btn color="warning" @click="askforid()">Actualizar</v-btn>
      </v-form>

      <div class="borrarnoti">
        <h1>Gestionar Notifiaciones</h1>
        <v-form
          ref="formBorrarNotif"
          v-model="valid"
          lazy-validation
          id="miform">

          <v-text-field
            v-model="notification.id"
            :rules="rules.required"
            label="Id Notificacion"
            :append-icon="'mdi-card-account-details'"
          ></v-text-field>
          <v-btn color="success" @click="showNoti()">Previsualizar</v-btn>
          <v-btn color="error" @click="deletenotification()">Eliminar</v-btn>
        </v-form>
      </div>
    </v-card>
  </div>
</template>

<script>
var findUser
var idtodelete
const url_api = 'http://localhost:3001/recordatorios/'
export default {
  components: {},

  data: () => ({
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
  }),

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
            text: 'Se agrego la notificacion correctamente con id: '+ response.id,
          })
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

    deletenotification() {
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
              let url = 'http://localhost:3001/recordatorios/' + this.notification.id
              await this.$axios.delete(url)
              this.$refs.formBorrarNotif.reset()
              this.$swal.fire({
                type: 'success',
                title: 'Operación exitosa.',
                text: 'La notifiacion se eliminó correctamente.',
              })
            } catch (error) {
              this.$swal.fire({
                type: 'error',
                title: 'Error',
                text: 'No se encontro esta notificacion',
              })
            }
          }
        })
    },

    async showNoti() {
      try {
        //
        let response = await this.$axios.get(
          'http://localhost:3001/recordatorios/' + this.notification.id
        )
        this.noti = response.data
        this.$swal.fire({
                type: 'success',
                title: this.noti.title,
                text: this.noti.msg,
              })
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
.borrarnoti{
    margin-top: 10%;
    width: 50%;
    margin-left: 25%;
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