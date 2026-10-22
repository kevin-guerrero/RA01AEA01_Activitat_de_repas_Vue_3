<script setup>
import { computed, ref } from 'vue';

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
        escoltada: true
    }
]);

// Variable per el input de l'usuari
const newSong = ref('');

// Variable per les cançons escoltadas
const isListened = ref(false);

// Funcion per afegir una nova cançó
const createSong = () =>{
    songs.value.push({
        id: Date.now(), // Temps actual en millisegons
        nom: newSong.value, // Nom escollit per l'usuari
        escoltada: false // Per defecte la posem en false
    });

    // Limpiar input
    newSong.value = ''
};

// Funció per mostrar canços escoltadas
const songsListened = computed(() => {
    if(isListened.value === true) {
        return songs.value.filter(song => song.escoltada)
    }else {
        return songs.value
    }
});

</script>

<template>
  <h1>Gestor de canços</h1>
  <input v-model="newSong" placeholder="Escriu una nova canço">
  <button @click="createSong">Afegir</button>  

  <label>
    Mostrar canços escoltades
    <input type="checkbox" v-model="isListened">
  </label>

  <ul>
    <li 
     v-for="song in songsListened" 
     :key="song.id"
    >
     {{ song.nom }} -
     <span v-if="song.escoltada === true">Escoltada</span>
     <span v-else="song.escoltada === false">No Escoltada</span>
    </li>

  </ul>
</template>

<style scoped></style>
