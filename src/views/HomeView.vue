<script setup>
import { ref } from 'vue';
import Card from "../components/Card.vue"

let character = ref([])

async function loadCharacters() {
  const response = await fetch (`https://rickandmortyapi.com/api/character?page=1`);
  const data = await response.json();
  character.value = data.results;
  console.log(data);
}

loadCharacters()
</script>

<template>
  <div class="flex justify-center mt-10">
    <h1 class="text-5xl">Personajes de Rick y Morty</h1>
    
      <button><</button>
      <button>></button>  
  </div>
  <br><br>
  <div v-for="personaje in character" :key="character.id">{{ personaje.name }}

  </div>
  
  <Card/>
</template>
