<script setup>
import { ref } from 'vue';
import Card from "../components/Card.vue"
import { Icon } from '@iconify/vue';

let character = ref([])
let page = ref(1)

function nextPage() {
  page.value++
  loadCharacters()
}
function previousPage() {
  page.value--
  if (page.value<1){
    page.value.value=1
  }
  loadCharacters()
}



async function loadCharacters() {
  const response = await fetch (`https://rickandmortyapi.com/api/character?page=${page.value}`);
  const data = await response.json();
  character.value = data.results;
  console.log(data);
}

loadCharacters()
</script>

<template>
  <div class="m-8" id="container">
    <div class="flex justify-center mt-10 mb-10">
      <h1 class="text-5xl">Personajes de Rick y Morty</h1>
    </div>
  </div>


    
    <div class="grid grid-cols-2 gap-4 lg:grid-cols-4">
      <router-link v-for="personaje in character" :key="character.id" class="flex justify-center text-center" :to="`/${personaje.id}`">  
        <Card :character="personaje"/>
      </router-link>
    </div>

    
      <div class="flex flex-row justify-around btn m-4">
        <button class="hover:bg-gray-200 hover:transition bg-gray-300 flex flex-row rounded-xl text-center p-4" @click="previousPage" :disabled="page===1"><Icon class="text-3xl"icon="charm:arrow-left" /></button>
          <div>{{ page }}</div>
        <button class="hover:bg-gray-200 hover:transition bg-gray-300 flex flex-row rounded-xl text-center p-4" @click="nextPage"><Icon class="text-3xl align-text-bottom" icon="charm:arrow-right" /></button>      
      </div>
  
</template>
