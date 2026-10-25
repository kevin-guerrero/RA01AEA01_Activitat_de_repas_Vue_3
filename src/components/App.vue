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
    },
    {
        id: 3,
        nom: "Chasing Cars",
        escoltada: false
    },
    {
        id: 4,
        nom: "Hey Jude",
        escoltada: true
    }
]);

// Variable per el input de l'usuari
const newSong = ref('');

// Variable per les cançons que falten per escoltar
const isListened = ref(false);

// Funcion per afegir una nova cançó
const createSong = () =>{

    // Si l'usuari insereix una cadena de text buida es descarta
    if(newSong.value.trim() === '') {
        newSong.value = '' // Netejar input
        return 
    }

    songs.value.push({
        id: Date.now(), // Temps actual en millisegons
        nom: newSong.value, // Nom escollit per l'usuari
        escoltada: false // Per defecte la posem en false
    });

    // Netejar input
    newSong.value = ''
};

// Funció per mostrar canços que falten per escoltar
const songsListened = computed(() => {
    if(isListened.value === false) {
        return songs.value
    }else {
        return songs.value.filter(song => song.escoltada === false)
    }
});

const changeStatus = (songSelected) => {
    //Buscar canço seleccionada
    const songSearch = songs.value.find(song => song.id === songSelected);

    // Canviar valor (boolean) de la propietat (escoltada) del objecte (cançó)
    songSearch.escoltada = !songSearch.escoltada;
}

const deleteSong = (songSelected) => {
    const songsUpdated = songs.value.filter(song => song.id !== songSelected)

    songs.value = songsUpdated
}

const totalSongs = computed(() => {
    var allSongs = 0;

    for(const song of songs.value) {
        allSongs++
    };

    return allSongs;
});

const pendingSongs = computed (() => {
    var songPending = 0;

    for(const song of songs.value) {
        if(song.escoltada === false) {
            songPending++
        }
    };

    return songPending;
});

</script>

<template>
  <h1>Gestor de cançons</h1>
  <input v-model="newSong" placeholder="Escriu una nova cançó">
  <button @click="createSong">Afegir</button>  

  <label>
    Mostrar cançons pendents
    <input type="checkbox" v-model="isListened">
  </label>

  <ul>
    <li 
     v-for="song in songsListened" 
     :key="song.id"
    >
     {{ song.nom }} -
     <button v-if="song.escoltada" @click="changeStatus(song.id)">Escoltada</button>
     <button v-else @click="changeStatus(song.id)">No Escoltada</button>
     <button @click="deleteSong(song.id)">🗑️</button>
    </li>
  </ul>

  <p >Total: {{ totalSongs }} | Pendents: {{ pendingSongs }} </p>
</template>

<style scoped></style>
