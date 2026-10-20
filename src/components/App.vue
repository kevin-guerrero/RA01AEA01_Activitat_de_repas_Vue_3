<script setup>
import { ref } from 'vue';

// Info
const songs = ref([
    {
        id: 1,
        nom: "Ultraviolence",
        escoltada: false
    },
    {
        id: 2,
        nom: "Cinnamon girl",
        escoltada: false
    }
])

const createSong = () =>{
    songs
}

</script>

<template>
  <h1>Gestor de canços</h1>
  <input v-model="nom" placeholder="Escriu una nova canço">
  <button @click="createSong()" >Afegir</button>  

  <ul>
    <li v-for="song in songs" :key="song.id">
        {{ song.nom }} - {{ song.escoltada }}
    </li>
  </ul>
</template>

<style scoped></style>
