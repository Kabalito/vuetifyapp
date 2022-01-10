<template>
  <v-card dark>
    <v-img :src="album.photoURL" height="200px">
      <v-card-title class="text-h5">{{ album.title }}</v-card-title>
    </v-img>
    <v-card-actions>
        <v-spacer/>
      <v-btn icon @click="esFavorito = !esFavorito">
        <v-icon class="mr-1" :color="esFavorito? 'red' : ''"> mdi-heart </v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon class="mr-1"> mdi-share-variant </v-icon>
      </v-btn>
      
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: ["album"],
  data(){
      return{
          esFavorito: false,
      }
  }
};
</script>

<style></style>
