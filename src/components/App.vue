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
]);

// Variable per el input de l'usuari
const newSong = ref('');

// Funcion per afegir una nova cançó
const createSong = () =>{
    songs.value.push({
        id: Date.now(), // Temps actual en millisegons
        nom: newSong.value, // Nom escollit per l'usuari
        escoltada: false // Per defecte la posem en false
    });
};

</script>

<template>
  <h1>Gestor de canços</h1>
  <input v-model="newSong" placeholder="Escriu una nova canço">
  <button @click="createSong">Afegir</button>  

  <ul>
    <li 
     v-for="song in songs" 
     :key="song.id"
    >
     {{ song.nom }} - {{ song.escoltada }}
    </li>
  </ul>
</template>

<style scoped></style>
