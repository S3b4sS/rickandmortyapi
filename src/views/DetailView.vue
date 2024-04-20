<template>
  <div class="grid grid-cols-2 gap-4 lg:grid-cols-4">
    <router-link v-for="personaje in character" :key="character.id" class="flex justify-center text-center"
      :to="`/${personaje.id}`">
      <Card :character="personaje" />
    </router-link>
  </div>

  <div v-if="character"
    class="about m-2 flex flex-col mt-2 mb-2 font-bold overflow-hidden rounded-xl shadow-xl bg-slate-600"
    id="container">
    <div class="flex ">

      <router-link :to="'/'">
        <button
        class="hover:bg-gray-200 hover:transition bg-gray-300 rounded-xl flex flex-row items-center justify-center font-bold h-11 w-11"
        @click="previousPage" :disabled="page === 1"><Icon class="text-3xl"icon="charm:arrow-left" /> </button>
      </router-link>
    </div>
      
    <div>{{ page }}</div>

    <h1 class="m-2 text-5xl font-bold text-center">Hola tonotos, esta es la informacion de {{ character.name }}</h1>

    <div class="m-2 flex justify-left mt-2 mb-2 font-semibold flex-around overflow-hidden rounded-xl shadow-xl bg-white"
      id="container">
      <div class="m-2 ">
        <img class="rounded-xl" :src="character.image" alt="" srcset="">
      </div>
      <div class="m-2 text-2xl flex flex-col justify-evenly   ">
        <p>Species: {{ character.species }}</p>
        <p>Gender: {{ character.gender }} </p>
        <p>Status: {{ character.status }}</p>
        <p>Located at {{ character.location.name }}</p>
        <p>Origin's from {{ character.origin.name }}</p>


          <div class="flex flex-row justify-around btn m-4">
            <button class="hover:bg-gray-200 hover:transition bg-gray-300 flex flex-row rounded-xl text-center p-4" @click="like" :disabled="page===1"><Icon icon="charm:thumb-up"  style="color: #00ff2a" /></button>
              <div>{{ page }}</div>
            <button class="hover:bg-gray-200 hover:transition bg-gray-300 flex flex-row rounded-xl text-center p-4" @click="dislike"><Icon icon="charm:thumb-down"  style="color: #ff0000" /></button>      
          </div>
      </div>
    </div>

  </div>
  <div>
    <LikeView />
  </div>
</template>

<script setup>

import { useRoute } from 'vue-router';
import { onMounted, ref } from "vue";
import { Icon } from '@iconify/vue';
import LikeView from './LikeView.vue';

export default {
  components: {
    LikeView,
  },
};

const route = useRoute()
const characterId = route.params.id
const character = ref(null)

onMounted(async () => {
  try {
    const response = await fetch(`https://rickandmortyapi.com/api/character/${characterId}`);
    const data = await response.json();
    character.value = data
    console.log(data);

  } catch (error) {

  }
})

function like() {
  like.value++
  
}
function dislike() {
  dislike.value++
  
}
</script>

<style>
body {
  background-color: lightslategrey;
}
</style>