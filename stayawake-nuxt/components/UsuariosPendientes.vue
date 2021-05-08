<template>
  <v-card>
    <v-card-actions>
      <h1 class="acheuno">Usuarios pendientes de aprobación</h1>
      <v-spacer></v-spacer>
      <v-btn color="success">Crear usuario</v-btn>
    </v-card-actions>

    <v-card-text>
      <v-data-table
        :headers="headers"
        :items="users"
        :items-per-page="5"
        class="elevation-1"
      >
        <template v-slot:item.actions="{ item }">
          <v-icon class="mr-2" @click="aprobarUsuario(item)">
            mdi-checkbox-marked-circle
          </v-icon>
          <v-icon @click="rechazarUsuario(item)"> mdi-delete </v-icon>
        </template>
      </v-data-table>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      headers: [
        {
          text: 'ID',
          align: 'start',
          sortable: true,
          value: 'id',
        },
        { text: 'Nombre', value: 'name' },
        { text: 'Apellido', value: 'lastName' },
        { text: 'Email', value: 'email' },
        { text: 'Contraseña', value: 'password' },
        { text: 'Acciones', value: 'actions' },
      ],
      users: [],
    }
  },

  beforeMount() {
    this.getUsers()
  },

  methods: {
    async getUsers() {
      try {
        let response = await this.$axios.get(
          'http://localhost:3001/usuarios?pending=true'
        )
        this.users = response.data
      } catch (error) {
        console.error(error)
      }
    },

    async aprobarUsuario(findUser) {
      // Crear un nuevo objeto con la info del usuario

      try {
        findUser.pending = false
        let user = Object.assign({}, findUser)
        let response = await this.$axios.put(
          'http://localhost:3001/usuarios/' + findUser.id,
          user
        )
        console.log(user.pending)
        this.$swal.fire({
          type: 'success',
          title: 'Operación exitosa.',
          text: 'Usuario aprobado.',
        })
        this.getUsers()
      } catch (error) {
        this.$swal.fire({
          type: 'error',
          title: 'Error.',
          text: 'Hubo un problema al aceptar al usuario',
        })
      }
    },

    rechazarUsuario(User) {
      this.$swal
        .fire({
          type: 'warning',
          title: '¿Está seguro de rechazar el usuario?',
          text:
            'En caso de tratarse de un error deberá modificarlo manualmente.',
          allowEscapeKey: false,
          allowOutsideClick: false,
          showCancelButton: true,
        })
        .then(async (result) => {
          if (result.value) {
            try {
              User.deleted = 1
              User.pending = false
              let response = await this.$axios.put(
                'http://localhost:3001/usuarios/' + User.id,
                User
              )
              this.$swal.fire({
                type: 'success',
                title: 'Operación exitosa.',
                text: 'El usuario se descartó correctamente.',
              })
              this.getUsers()
            } catch (error) {
              this.$swal.fire({
                type: 'error',
                title: 'Ha ocurrido un problema al descartar',
                text: error.toString(),
              })
            }
          }
        })
    },
  },
  components: {},
}
</script>

<style>
.acheuno {
  color: black;
}
</style>