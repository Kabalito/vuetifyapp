<template>
  <v-app>
    <v-app-bar dense color="blue" dark app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Title</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn text @click="dialogRegistro = !dialogRegistro"> Registro </v-btn>
        <v-btn icon>
          <v-icon>mdi-bell</v-icon>
        </v-btn>
      </v-toolbar-items>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" app>
      <v-list>
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://randomuser.me/api/portraits/men/43.jpg"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title>Jeffrey Lawrence</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>
        <v-list-item-group v-model="selectedItem" color="primary">
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-account</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Usuarios</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-image-album</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Album</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-icon>
              <v-icon color="red">mdi-heart</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Favoritos</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-cog</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Configuracion</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
    <!--CONTENIDO-->
    <v-main class="mt-5">
      <vistas-usuarios />
    </v-main>
    <!--  Dialog  -->
    <v-dialog v-model="dialogRegistro" width="500">
      <v-card>
        <v-card-title class="text-h5 grey lighten-5"> Registro </v-card-title>
        <v-card-text>
          <v-form v-model="valido">
            <v-text-field
              label="Nombre Completo"
              hint="Ejemplo: Luis Amaya"
              :rules="reglasNombre"
              :counter="maxCaracteres"
              v-model="nuevoUsuaro.nombre"
            >
            </v-text-field>
            <v-text-field
              label="Correo Electronico"
              hint="Ejemplo: kabalito@gmail.com"
              :rules="reglasCorreo"
              v-model="nuevoUsuaro.email"
            >
            </v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text :disabled="!valido"> Terminar </v-btn>
          <v-btn color="primary" text> limpiar </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import VistasUsuarios from "./vistas/VistasUsuarios.vue";

export default {
  name: "App",

  components: {
    VistasUsuarios,
  },

  data() {
    return {
      drawer: true,
      dialogRegistro: true,
      valido: false,
      maxCaracteres: 25,
      nuevoUsuaro: {
        nombre: "",
        email: "",
      },
      reglasNombre: [
        (v) => {
          if (v.length > 0) {
            return true;
          }
          return "debe escribir un correo electronico";
        },
        (v) => {
          if (v.length <= this.maxCaracteres) {
            return true;
          }
          return `Debe ingresar menos de ${this.maxCaracteres} caracteres`;
        },
      ],
      reglasCorreo: [
        (v) => {
          if (v.length > 0) {
            return true;
          }
          return "debe escribir un nombre";
        },
        (v) => {
          if(/.+@.+\..+/.test(v)){
            return true
          }
          return "debe escribir un correo electronico valido";
        },
      ],
    };
  },
};
</script>
