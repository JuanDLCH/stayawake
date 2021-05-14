<template>
  <v-card>
    <v-card-actions>
      <h1 class="acheuno">Rutas asignadas</h1>
      <v-spacer></v-spacer>
      <v-btn color="success" to="/rutas">Asignar ruta</v-btn>
    </v-card-actions>

    <v-card-text>
      <v-data-table
        :headers="headers"
        :items="routes"
        :items-per-page="5"
        class="elevation-1"
      >
        <template v-slot:item.actions="{ item }">
          <v-icon class="mr-2" @click="editRoute(item)"> mdi-pencil </v-icon>
          <v-icon @click="deleteRoute(item)"> mdi-delete </v-icon>
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
          text: 'IDConductor',
          align: 'start',
          sortable: true,
          value: 'idConductor',
        },
        { text: 'Fecha', value: 'fecha' },
        { text: 'Salida', value: 'salida' },
        { text: 'Llegada', value: 'llegada' },
        { text: 'Observacion', value: 'observation' },
        { text: 'Estado', value: 'estado' },
        { text: 'Acciones', value: 'actions' },
      ],
      routes: [],
    }
  },

  beforeMount() {
    this.getRoutes()
  },

  methods: {
    async getRoutes() {
      try {
        let response = await this.$axios.get('http://localhost:3001/rutas')
        this.routes = response.data
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

    deleteRoute(item) {
      this.$swal
        .fire({
          type: 'warning',
          title: '¿Está seguro de eliminar una ruta?',
          text: 'Ningún dato asociado a ella podrá recuperarse.',
          allowEscapeKey: false,
          allowOutsideClick: false,
          showCancelButton: true,
        })
        .then(async (result) => {
          if (result.value) {
            try {
              let url = 'http://localhost:3001/rutas/' + item.id
              await this.$axios.delete(url)
              this.$swal.fire({
                type: 'success',
                title: 'Operación exitosa.',
                text: 'La ruta se eliminó correctamente.',
              })
              this.getRoutes()
            } catch (error) {
              this.$swal.fire({
                type: 'error',
                title: 'Error',
                text: 'No se encontró esta ruta',
              })
            }
          }
        })
    },

    async editRoute(item) {
      this.$router.push('rutas/' + item.id)
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