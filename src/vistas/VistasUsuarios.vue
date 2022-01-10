<template>
  <v-container>
    <v-row wrap>
      <v-col cols="12" md="12">
        <v-data-table
          :items="usuarios"
          :headers="cabeceras"
          :items-per-page="4"
          :search="busqueda"
        >
          <template v-slot:top>
            <v-text-field
              v-model="busqueda"
              label="Filtrar por Nombre"
              class="mx-4"
            ></v-text-field>
          </template>
          <template slot="no-data">
            <p>No hay usuarios registrados por ahora</p>
          </template>
          <template v-slot:item.image="{ item }">
            <td>
              <v-avatar>
                <img :src="item.image" />
              </v-avatar>
            </td>
          </template>
          <template v-slot:item.acciones="{ item }">
            <td class="text-center">
              <v-btn icon v-model="item.acciones" @click="editar(item)">
                <v-icon color="green">mdi-pencil</v-icon>
              </v-btn>
              <v-btn icon v-model="item.acciones" @click="eliminarUsuario(item)">
                <v-icon color="red">mdi-delete</v-icon>
              </v-btn>
            </td>
          </template>
        </v-data-table>

        <!-- DIALOG -->

        <v-dialog v-model="dialog" width="500">
          <v-card>
            <v-card-title class="text-h5 grey lighten-2">
              Editar Usuario
            </v-card-title>

            <v-card-text>
              <v-text-field
                label="Nombre Completo"
                v-model="usuarioEditar.nombre"
              ></v-text-field>
              <v-text-field
                label="Correo Electronico"
                v-model="usuarioEditar.email"
              ></v-text-field>
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="terminarEdicion">
                Terminar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  methods: {
    buscarUsuario(id) {
      for (var i = 0; i < this.usuarios.length; i++) {
        if (this.usuarios[i].id === id) {
          return i;
        }
      }
      return -1;
    },

    

    editar(usuario) {
      this.usuarioEditar.nombre = usuario.nombre;
      this.usuarioEditar.id = usuario.id;
      this.usuarioEditar.email = usuario.email;
      this.dialog = !this.dialog;
    },

    eliminarUsuario(usuario) {
      var index = this.buscarUsuario(usuario.id)
      if(index !== -1) {
        var eliminacionConfirmada = confirm(`Esta Seguro que quiere eliminar el usuario con correo ${usuario.email}`)
        if(eliminacionConfirmada){
          this.usuarios.splice(index, 1)

        }
      }
    },

    terminarEdicion() {
      var indexUsuario = this.buscarUsuario(this.usuarioEditar.id)
      var usuario = this.usuarios[indexUsuario]
      usuario.nombre = this.usuarioEditar.nombre;
      usuario.email = this.usuarioEditar.email;
      this.usuarioEditar.nombre = "";
      this.usuarioEditar.email = "";
      this.dialog = false;
    },
  },

  data() {
    return {
      busqueda: "",
      dialog: false,
      usuarioEditar: {
        id: 0,
        nombre: "",
        email: "",
      },
      usuarios: [
        {
          id: 12,
          nombre: "Daisy Mendoza",
          image: "https://randomuser.me/api/portraits/women/12.jpg",
          email: "daisy.mendoza@example.com",
        },
        {
          id: 7,
          nombre: "Christine Davis",
          image: "https://randomuser.me/api/portraits/women/7.jpg",
          email: "Christine-Davis@example.com",
        },
        {
          id: 26,
          nombre: "Layla Weaver",
          image: "https://randomuser.me/api/portraits/women/26.jpg",
          email: "Layla.Weaver@example.com",
        },
        {
          id: 4,
          nombre: "Katrina Gutierrez",
          image: "https://randomuser.me/api/portraits/women/4.jpg",
          email: "katrina.gutierrez@example.com",
        },
        {
          id: 37,
          nombre: "Marian Montgomery",
          image: "https://randomuser.me/api/portraits/women/37.jpg",
          email: "marian.montgomery@example.com",
        },
        {
          id: 8,
          nombre: "Ethan Ford",
          image: "https://randomuser.me/api/portraits/men/8.jpg",
          email: "ethan.ford@example.com",
        },
        {
          id: 54,
          nombre: "Christopher Ray",
          image: "https://randomuser.me/api/portraits/men/54.jpg",
          email: "christopher.ray@example.com",
        },
      ],
      cabeceras: [
        {
          text: "Foto",
          sortable: false,
          value: "image",
        },
        {
          text: "Nombre Completo",
          value: "nombre",
          sortable: true,
        },
        {
          text: "Correo Electronico",
          value: "email",
          sortable: true,
        },
        {
          text: "Acciones",
          align: "center",
          sortable: false,
          value: "acciones",
        },
      ],
    };
  },
};
</script>

<style></style>
