<script setup>
import { ref } from 'vue';
const missatge = ref('Completar')
const canviarMissatge = () => {
  missatge.value = 'Desmarcar'
}
</script>

<template>
  <div>
    <h1>{{ missatge }}</h1>
    <button @click="canviarMissatge">Canvia el missatge</button>
  </div>

  <h1>You did it!</h1>
  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>
</template>

<style scoped></style>
