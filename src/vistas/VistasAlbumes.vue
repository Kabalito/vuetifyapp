<template>
    <v-container > 
        <v-row >
            <v-col cols="12" md="6" v-for="(album, i) in albumes" :key="i" >
                <album :album="album"/>

            </v-col>
        </v-row>
    </v-container>     
</template>

<script>
import Album from '../components/Album.vue'
export default {

  components: { Album },

    data(){
        return {
            albumes: [
                {
                title: 'Viajes',
                photoURL: "https://picsum.photos/id/555/640/480",
                },
                {
                title: 'Bosques',
                photoURL: "https://picsum.photos/id/486/640/480",
                },
                {
                title: 'Que es eso',
                photoURL: "https://picsum.photos/id/987/640/480",
                },
                {
                title: 'Ciudades',
                photoURL: "https://picsum.photos/id/894/640/480",
                },
                {
                title: 'Centros',
                photoURL: "https://picsum.photos/id/987/640/480",
                },
                {
                title: 'Plazas',
                photoURL: "https://picsum.photos/id/368/640/480",
                },
                {
                title: 'Personas',
                photoURL: "https://picsum.photos/id/123/640/480",
                },
                {
                title: 'Momentos',
                photoURL: "https://picsum.photos/id/455/640/480",
                },
            ]
        }
    }

}
</script>

<style>

</style>